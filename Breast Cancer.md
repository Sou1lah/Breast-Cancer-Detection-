#  Breast Cancer — Overview

## What is Cancer?

The human body consists of trillions of cells that grow, divide, and die in an orderly manner. Cancer occurs when a cell's DNA is damaged, causing it to divide uncontrollably without dying as normal cells do. These abnormal cells accumulate and form a **tumor**.

Not all tumors are dangerous:
- **Benign tumor** — grows slowly, does not spread, generally not life-threatening
- **Malignant tumor** — invasive cancer that can spread to surrounding tissue and distant organs (a process called **metastasis**)

---

## What is Breast Cancer?

Breast cancer is characterized by the formation of malignant tumors in breast tissue. It most commonly originates in the **milk ducts** or **lobules** of the breast.

Risk increases with age (notably after 40–50), though it can affect individuals of any age, predominantly women and rarely men.

**Key statistics:**
- Most common cancer among women worldwide
- Affects approximately 1 in 8 women over a lifetime
- Early-stage survival rate exceeds 99%
- Survival rates decline significantly once the cancer has metastasized

---

## Detection Methods

Several imaging modalities are used in clinical practice:

**1. Mammography (X-ray)**
- Primary screening tool
- Uses low-dose X-rays to image breast tissue
- Capable of detecting tumors before they are physically palpable

**2. Ultrasound**
- Uses sound waves to generate images
- Effective at differentiating fluid-filled cysts from solid masses
- Modality used in the BUSI dataset

**3. MRI**
- Highest detail imaging modality
- Reserved for high-risk patients due to cost and scan duration

**4. Biopsy**
- Not an imaging technique — involves physical extraction of tissue for microscopic analysis
- Considered the **ground truth** for diagnosis
- Forms the basis for dataset labels (benign / malignant)

---

## What Medical Images Reveal

Radiologists examine mammograms and ultrasounds for the following findings:

| Finding | Clinical Significance |
|---|---|
| **Mass / lump** | Solid area — may be benign or malignant |
| **Calcifications** | Calcium deposits — certain patterns are associated with malignancy |
| **Architectural distortion** | Inward pulling of tissue — a suspicious indicator |
| **Asymmetry** | Structural difference between breasts |

---

## The ML Classification Problem

Breast cancer datasets typically label images into three categories:

- **Normal** — no pathological findings
- **Benign** — tumor present, non-cancerous
- **Malignant** — cancerous tumor

This project frames the task as a **3-class classification problem**, where the model learns to assign an image to one of these categories.

---

## Challenges for Machine Learning

| Challenge | Description |
|---|---|
| **Class imbalance** | Cancer cases are significantly underrepresented in real-world data |
| **Visual similarity** | Benign and malignant cases can appear nearly identical |
| **High stakes** | A false negative (missed cancer) carries serious clinical consequences |
| **Limited data** | Labeled medical datasets are expensive and scarce |

---

## Key Terminology

| Term | Definition |
|---|---|
| Tumor | Abnormal mass of cells |
| Benign | Non-cancerous |
| Malignant | Cancerous |
| Mammogram | X-ray image of the breast |
| Metastasis | Spread of cancer to other organs |
| False Negative | Model predicts no cancer when cancer is present — clinically dangerous |
| False Positive | Model predicts cancer when none exists |
| AUC-ROC | Standard evaluation metric for medical classification models |