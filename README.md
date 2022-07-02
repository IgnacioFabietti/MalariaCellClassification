# Malaria Detection in Cells 

### Problem Statement
This problem comes from comes from a 2021 Kaggle Dataset, details [here]([https://www.kaggle.com/datasets/iarunava/cell-images-for-detecting-malaria](https://www.kaggle.com/datasets/iarunava/cell-images-for-detecting-malaria)) . The official problem statement for this Kaggle is, “Save humans by detecting and deploying Image Cells that contain Malaria or not!”

### Background
Malaria is an acute febrile illness caused by _Plasmodium_ parasites, which are spread to people through the bites of infected female _Anopheles_ mosquitoes. According to the latest [World malaria report,](https://www.who.int/publications-detail-redirect/9789240040496) there were 241 million cases of malaria in 2020 compared to 227 million cases in 2019. The estimated number of malaria deaths stood at 627 000 in 2020 – an increase of 69 000 deaths over the previous year.

Accurate parasite counts are essential to diagnosing malaria correctly, testing for drug-resistance, measuring drug-effectiveness, and classifying disease severity. However, microscopic diagnostics is not standardized and depends heavily on the experience and skill of the microscopist.  It is common for microscopists in low-resource settings to work in isolation, with no rigorous system in place that can ensure the maintenance of their skills and thus diagnostic quality.

### Goal
By training a convolutional neural network, we want to predict whether a cell has been infected with malaria based on a microscopy image. By utilising an automatic parasite counter, we can:
-  Provide a more reliable and standardized interpretation of blood films.
-  Allows more patients to be served by reducing the workload of the malaria field workers.
-   Reduce diagnostic costs.

 Ultimately, we want to find ways we can use these predictions to developing countries and WHO utilise resources better. The effectiveness of our predictions will determine what kinds of things our predictions can be used for

### Methods

A total of 27558 RGB images composed the balanced dataset, that were scaled to [0,1] scale for the network training. We built an AlexNet CNN model, and used sparse categorical crossentropy loss, Adam optimiser, and accuracy as metric as it was a balanced dataset.

### Results 
The model converged after 9 epochs, where the validation loss was  0.1147 and the accuracy 0.9608.
The results of the test set were:
 Label|Correct Prediction|Incorrect Prediction|
-----------|---------|---------|
Uninfected|17%|34%|
Parasitized|45%|4%|

The model tends to classify uninfected cells as infected, meaning that there is a higher false positive than false negatives. In other words, 1 out of 4 healthy cells get categorised as parastized, whereas 1 in 10 of parasitised are categorised as healthy. So out of 400 cells under a microscrope
- 170 would test negative (150 correct and 20 false negatives)
- 230 would test positive (180 correct and 50 false positive)

### Recommendation
The labour cost of laboratory staff per hour is USD 6.80, and the average cost of diagnosis by microscopy takes 1 Hour to complete 
[(source)]([https://idpjournal.biomedcentral.com/articles/10.1186/s40249-020-00745-9])  .Our predictions can help speed up the time by hiding the cells that are not positive, so the microscopists can focus their attention to those that have been assigned the label.  As no meta-data was provided with patient information, we can't know the impact at  patient level classification.

### Risks and Assumptions

The subject pool was 200 subjects, with 50 healthy and 250 infected, from a population in Bangladesh. We can expect differences when tested on larger populations and of different regions such as the African continent. When deployed, regular check ups will tell if the model needs re-training, fine-tuning, on an upgrade to its architecture. This can be validated with the observed false positives and negatives that appear in the patient population, and can be contrasted with a specialist's review of the samples. 
The small CNN presented would allow it to be deployed on modern mobiles to aid people in the field, whereas those with more parameters or more complex architectures might struggle to be deployed for real-time classification. Nonetheless, the architecture can be benchmarked against other models across accuracy and computational time in the future.

### Data Dictionaries
Cell Data  from [NIH]([https://ceb.nlm.nih.gov/repositories/malaria-datasets/](https://lhncbc.nlm.nih.gov/))

Folder Name|Data Type|Description|Notes
-----------|---------|-----------|-----
Uninfected| Healthy Cells|13780 examples|Rounded Cells
Parasitized| Unhealthy Cells|13780 examples|Purple Spots
