# PV-Defect-Detection-YOLOv5-based

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
Several training sessions were run using all the data, increasing some specific ones. It was concluded that to maximize accuracy, it is better not to balance the data, leaving the maximum number of defects possible in PC and PCM (hotspot and multiple hotspot), and sacrificing accuracy in other classes. Best model to date:

> Train results:   
><img src="https://github.com/user-attachments/assets/e22e44f2-b626-4a2f-b5cb-02fe4db4cbd4" width="350">
><img src="https://github.com/user-attachments/assets/f05ec63c-2a52-4ec6-94d5-6aaf723f24cf" width="350">
><img src="https://github.com/user-attachments/assets/7fec486d-e04b-49e3-b696-b58d19ac7276" width="350">
><img src="https://github.com/user-attachments/assets/f99eba83-2d0c-4a6f-8b1d-f1691384f64c" width="350">

> Test results:  
> <img src="https://github.com/user-attachments/assets/bb2968fa-3469-4c74-9207-53c29768cbd0" width="350">
> <img src="https://github.com/user-attachments/assets/248407b7-3262-4d4a-b019-7285a2dc1c2e" width="350">  
> As mentioned earlier, sacrificing accuracy in minority classes, we will now look at the performance.

## Performance 📈

<img src="https://github.com/user-attachments/assets/91ef4ac0-a116-4d1e-b5e0-47b86383d3eb" width="350">
<img src="https://github.com/user-attachments/assets/c8c3c393-af27-491a-8211-22c795db55f6" width="350">
<img src="https://github.com/user-attachments/assets/23c0bd57-9dc5-40f8-864e-28ef87c890d6" width="350">
<img src="https://github.com/user-attachments/assets/2aaf5378-4e74-45a6-8bde-f58792e094a2" width="350">
<img src="https://github.com/user-attachments/assets/28b00ed3-50be-43be-bb4c-cdc0e1192a8e" width="350">
<img src="https://github.com/user-attachments/assets/6839260a-8f90-463f-b765-20f5fe347b27" width="350">
<img src="https://github.com/user-attachments/assets/2de516c7-cc7f-49d8-a350-72b6d1de784f" width="350">

## Production deployment
For the production deployment, a web interface was created in Streamlit, which was launched on a specific server address so that the labeling team could easily connect by being on the same network. In the interface, the path to a folder was provided, and the labels with the predictions were automatically saved into it, in the format required by the labeling app. This way, the folder could be loaded directly, and the model's predictions could be modified without any additional adjustments. 

> Predictions loaded (frame with green lines where it made errors)
> Monopoles  
> <img src="https://github.com/user-attachments/assets/2c20afab-150d-4217-9dbb-b50e03e40a7e" width="300">  <img src="https://github.com/user-attachments/assets/b70e4643-f39c-42ca-bf75-53a61838c3ee" width="300">  

> Traditional plants  
> <img src="https://github.com/user-attachments/assets/3ceb2386-1798-4c9b-907a-e749f808206d" width="300">  <img src="https://github.com/user-attachments/assets/4977a786-145b-45ab-a9b6-c56ec2870180" width="300">  <img src="https://github.com/user-attachments/assets/602930d6-e8d9-44ee-bc0c-54069e7ff57f" width="300">

## Future work
❗The order of improvements is the one I consider should be addressed.
1. Upgrade to YOLOv10 => immediate improvement.
2. Obtain more samples of PA, PS, and BD, at least 2k for each of them.
3. Based on the tests and my experience, the target dataset for the thermal model is as follows (without data augmentation):  
>PCM: 12k
>PC: 12k
>BS: 8k
>BD: 2k
>PS: 2k
>PA: 2k

>>It is difficult to increase BD, PS, and PA without increasing PCM and PC because the photos usually don’t have only the first ones without including hotspots...

>>In BD, PS, and PA, with this amount of defects, the model learns very well, they are very easy to recognize. But I wouldn’t sacrifice variance or defects in PCM and PC to balance things out. It’s better to have a strong PC and PCM model than something mediocre that tries to capture a little bit of everything. I would prioritize accuracy in major classes, as I’ve done (the more plants in the data, the better; more data is always better).

5. Full pipeline objective:

>Thermal model with 6 classes (this could be replaced by two cascading models, one for detecting 4 classes (PC, PCM, BD, others) => others are passed to a classifier, the classifier only receives the bounding box corners of "others").

>⚠️ It is necessary to have visual and thermal data aligned.

>The classes PC and PCM, along with their labels, are passed to another classifier. This classifier is fed with the bounding box from the thermal image and the corresponding bounding box from the visual image (they must be aligned). With this, we will be able to be more specific about the defect. The idea is for the model to learn that PC + brown tones in the visual = dirt, and so on for each class.

>With this, we could have a pipeline with multiple cascading models. I believe that if done correctly, it can achieve very high accuracy, much better than now, even by adding more models. There are plenty of data in the NAS, we just need to recycle them for training.

>The first model, the current one, would be improved to YOLOv10, or even higher if available. As for the classification models, I would also keep YOLO.
    
