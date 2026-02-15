# PDF Learning using GAN - NO₂ Concentration Distribution

**Name:** Avneet Sandhu  
**Roll Number:** 102303289  

---

## Objective

To learn the unknown probability density function (PDF) of a transformed NO₂ concentration variable using a Generative Adversarial Network (GAN).

---

## Dataset

**Feature used:**
- **NO₂ concentration** (`no2` column)
- **Source:** Air quality monitoring dataset
- **Type:** Continuous numerical data representing Nitrogen Dioxide levels

---

## Transformation

The original variable `x` is transformed into:

```
z = x + aᵣ · sin(bᵣ · x)
```

**Where:**
- `aᵣ = 0.5 × (r mod 7)`
- `bᵣ = 0.3 × (r mod 5 + 1)`

**For roll number: 102303289**
- **aᵣ = 2.0**
- **bᵣ = 1.5**

**Final Transformation:**
```
z = x + 2.0 · sin(1.5 · x)
```

This transformation introduces non-linearity through the sine function, creating a complex distribution that the GAN must learn.

---

## Methodology

### 1. **Data Preprocessing**
   - Load NO₂ concentration data from the dataset
   - Handle missing values and outliers
   - Extract the `no2` column for analysis

### 2. **Transformation of NO₂ Values**
   - Apply the non-linear transformation: `z = x + 2.0 · sin(1.5 · x)`
   - Create a more complex distribution from the original data

### 3. **Standardization of Data**
   - Normalize the transformed data using Z-score normalization
   - Ensure data is in a suitable range for GAN training

### 4. **GAN Training**
   - **Generator Network:** 
     - Generates synthetic samples from random noise
     - Architecture: Fully connected layers with ReLU/LeakyReLU activations
   - **Discriminator Network:**
     - Distinguishes between real and fake samples
     - Architecture: Fully connected layers with LeakyReLU and Dropout
   - **Training Process:**
     - Adversarial training with alternating updates
     - Binary Cross-Entropy loss function
     - Adam optimizer for both networks

### 5. **Generation of Fake Samples**
   - Use the trained generator to produce synthetic samples
   - Generate large dataset (e.g., 10,000 samples) for analysis

### 6. **PDF Estimation using Kernel Density Estimation (KDE)**
   - Apply KDE to both real and generated samples
   - Use Gaussian kernel for smooth probability density estimation
   - Automatic bandwidth selection

### 7. **Comparison of Real vs GAN Learned Distribution**
   - Visual comparison through plots
   - Statistical comparison using metrics
   - Evaluation of distribution learning quality

---

## Results

### PDF Comparison
![PDF Comparison](results/pdf_comparison.png)

**Description:** This plot compares the probability density functions of the real transformed NO₂ data (blue) against the GAN-learned distribution (orange). The close alignment demonstrates the GAN's ability to accurately capture the underlying probability distribution.

---

### Histogram Comparison
![Histogram Comparison](results/histogram_comparison.png)

**Description:** Histogram overlay showing the frequency distribution of real samples versus GAN-generated samples. The overlapping bars indicate successful distribution matching across different value ranges.

---

### Zoomed PDF Comparison
![Zoomed PDF](results/zoomed_pdf_comparison.png)

**Description:** A detailed, zoomed-in view of the PDF comparison, highlighting the precision of the GAN-learned distribution in capturing subtle features, peaks, and tail behaviors of the real data distribution.

---

## Repository Structure

```
PDF_using_GAN_by_Avneet_Sandhu/
│
├── README.md                          
│
├── results/                          
│   ├── histogram_comparison.png      
│   ├── pdf_comparison.png            
│   └── zoomed_pdf_comparison.png    
│
├── Dataset.zip                       
│   └── data.csv                           
└── PDF_using_GAN.ipynb                         
```
---
