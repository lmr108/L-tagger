# L-tagger

<div style="display: flex; align-items: center; gap: 10px; flex-wrap: wrap;">
  <!-- Built for badge -->
  <img src="https://img.shields.io/badge/Built%20for-Eiffage%20Energia%20y%20Sistemas-blue" alt="Built for Eiffage Energia y Sistemas" />
  <img src="https://img.shields.io/badge/Status-in%20production-green" alt="Status: In production" />
  
  <!-- Confidentiality notice in a box -->
  <div style="border: 1px solid #ccc; padding: 6px 10px; border-radius: 4px; background-color: #f9f9f9;">
    <em>Sensitive code and data cannot be displayed due to company confidentiality.</em>
  </div>
</div>

<h4>Used Languages</h4>
<span> 
  <img src="https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54" />
</span>

<h4> Frameworks </h4>
<span>
  <img src="https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white">
</span>

## Description
-**Problem:** Inspecting thermographic images of photovoltaic panels required reviewing them one by one and manually labeling each defect, which is an extremely tedious task.

-**Solution:** Develop a model that automatically detects defects. To achieve this, we opted for transfer learning on a YOLO architecture. Below are more details and the model’s performance.

## Details
- **Development time:** 250 hours  
- **Hardware:** RTX 2080 ti x2
- **Frameworks & versiones:** CUDA: 11.8 | cuDNN: 8.7 | torch: 2.6.0+cu118 | Python: 3.12.10
- **Training time:** ~15h

## Data Collection
Since manual labeling was carried out over several years, a wide variety of data and labels were available. However, due to the specific processing of the images, not all could be reused. A meticulous selection process was carried out as follows:

> ```python
>script_1.py
>```
> Collected data from valid plants on the server (photos and labels) and saved them in a target location (for every 2 photos with defects in the dataset, another one without defects was introduced).
>
> > ```python
> >script_2.py
> >```
> > Processed all the collected plant data, allowing the creation of datasets of all kinds, while keeping only the defects that were desired (with the aim of conducting different tests). The images were automatically transferred to the correct folder structure, and the labels were normalized and prepared in YOLO format.
> > > ❗ The dataset mainly consisted of plants with monopoles and fewer traditional plants, which was reflected in the performance for each type, as we will see later ❗
> > > > Summary:
> > > > - **Total photos:**  8649 ==> **with defects:** 6086 | **without defects:** 2563
> > > >  ![image](https://github.com/user-attachments/assets/06771cab-4805-4ddd-ba3e-6e137c282673)
> > > > The most typical defects predominate over others
> > > > > Some classes depend on others, e.g., shadow is reflected as a hotspot, dirt is a hotspot, PID is reflected as PCM. The main classes are:  
> > > > > ![image](https://github.com/user-attachments/assets/53ac3977-0898-4e20-86e5-c7f43aa9c3ff)
> > > > > ![image](https://github.com/user-attachments/assets/f0a1b8d8-2d09-421d-9216-f0f1d0cd5582)
> > > > > ![image](https://github.com/user-attachments/assets/08808340-ca5c-40b8-9af0-36bf4285c0f6)
> > > > > ![image](https://github.com/user-attachments/assets/36289bf3-11c1-4c22-81d9-212f9cdd2b80)
> > > > > ![image](https://github.com/user-attachments/assets/279e49b9-0c84-4144-89f5-57df850c2cc8)







## Training


## Performance 📈

## Future work

## Model
