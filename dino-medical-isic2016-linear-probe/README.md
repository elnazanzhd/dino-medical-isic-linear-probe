# DINOv2 Linear Probe on ISIC 2016  
*Exploring self-supervised Vision Transformers for medical image understanding*

 
**Can a self-supervised Vision Transformer (DINOv2)** — trained only on natural images —  
**understand medical images without any finetuning?**

To explore this, I freeze the **DINOv2 ViT-S/14** encoder and train only a **single linear layer** on top of its embeddings (a “linear probe”).  
The goal is not to build a production melanoma detector, but to see how far **pure representation learning** can go on a real clinical dataset.

---

##  Dataset — ISIC 2016 (Task 3)
- 900 dermoscopic skin lesion images  
- Binary classification: **benign vs malignant**  
- Real-world class imbalance  
- Diverse imaging conditions (skin tone, lighting, lesion shape)

> Images are not included in this repo due to licensing.  
> Download from the official ISIC 2016 Challenge website and place them under `data/images/`.

---

##  Why DINOv2?
DINOv2 is a **self-supervised Vision Transformer** trained without labels.  
It learns general visual structure simply by predicting consistent representations across augmented views.

This makes it extremely powerful as a **frozen feature extractor** — even for domains it has never seen, including medical imaging.

---

## Results (Linear Probe Only)

| Metric | Score |
|--------|--------|
| **Accuracy** | **0.8333** |
| **F1-score** | **0.5161** |

DINOv2 embeddings transfer surprisingly well to dermoscopy, especially considering:

- No finetuning  
- Small dataset  
- Strong class imbalance  
- Only a single linear layer was trained  

---

##  Visualizations

### t-SNE of DINOv2 embeddings  
Shows partial separation of benign vs malignant lesions:

`figure/tsne_dino_isic.png`

### Sample predictions  
Examples (correct = green, incorrect = red) are in:

`/samples/`

---

##  How to Run

```
pip install -r requirements.txt
```

Download ISIC 2016 Task 3

```
adjust directories in the notebook
```

Then run it

```



##  About This Project
I built this to explore **self-supervised representation learning** beyond my usual UNet-based segmentation work.  
It’s a compact experiment that shows how much a modern Vision Transformer already “knows” — even before finetuning.
