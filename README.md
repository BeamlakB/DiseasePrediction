# DiseasePrediction Model

Throughout the past 20 years, people have browsed the web for health information to understand their symptoms and explore possible diagnoses. These tools empower patients to advocate for themselves and soothe anxiety and stress associated with health concerns. However, these websites can often provide misleading or incorrect information. As a result, patients might adopt harmful practices or treatments, delaying proper medical care.

## Project Goal

Our goal is to create a solution that provides trustworthy health information. We have developed a model that offers a concise list of diseases that may describe the given symptoms. 

### Example Symptom

- **Symptom:** "My skin has been breaking out in a terrible rash lately. Blackheads and pus-filled pimples abound on it. Additionally, my skin has been scurrying a lot."
- **Diagnosis:** **Acne**

## Project Overview
<img width="1240" height="490" alt="Dis-overview" src="https://github.com/user-attachments/assets/4334b2de-79d1-4f11-bcf9-333031aadeba" />

Our project aims to develop a model using patient-reported symptoms to predict potential diseases, offering individuals guidance on their health concerns before medical consultation.


### Data Collection and Processing

We gathered data from diverse sources, such as electronic health records and medical literature repositories. This data was meticulously pre-processed to ensure accuracy and reliability.

#### User Input          &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;               Domain knowledge Dataset  


<img width="244" height="116" alt="data1" src="https://github.com/user-attachments/assets/73f6c146-7526-4f27-8913-386fec2254c3" /> &emsp;&emsp;
<img width="287" height="145" alt="data2" src="https://github.com/user-attachments/assets/69dd12ef-6cf8-4b1c-a711-4af2ac634c3e" />



### Model Development

We utilized the LLAMA large language model for symptom extraction through prompt engineering. Followed by Information Retrieval, which we use to identify correlations between symptom combinations and diseases.
We experimented with a zero-shot prompt; however, the output wasn't as expected. Then we tried few-shot prompting, providing one example gave the expected output and, therefore we didn’t increase the number of examples.
```
[INST]
<<SYS>>
 Extract main symptoms from the sentence above and retrun them only as a list ?
<</SYS>>
 Text: I have been experiencing a skin rash on my arms, legs, and torso for the past few weeks. It is red, itchy,
      and covered in dry, scaly patches.
[/INST]
 ["skin_rash", "red_skin", "itchy", "dry", "scaly_patches"]
[INST]
 I have been experiencing joint pain in my fingers, wrists, and knees. The pain is often achy and throbbing,
 and it gets worse when I move my joints.
[/INST]

```

LLAMA output 
```
["rash", "pus-filled_pimples", "blackheads", "skin_scurling"]
```
### Result

We are using a few metrics to evaluate our TF-IDF algorithm performance. Accuracy will be a primary metric offering a high-level overview of the model’s predictive capability. We have also recorded a confusion Matrix. 
Table below provides the accuracy of each top-k result we experimented with. From our results, we can observe that 67% percent of the time the disease predicted was in thetop 10 ranked disease. We tested on 900 data entries.

### Table 3: Accuracy and Confusion Matrix

| Top-k | Accuracy | Correct Class | Incorrectly Class |
|-------|----------|---------------|-------------------|
| 3     | 38.4%    | 346           | 554               |
| 5     | 43.7%    | 394           | 506               |
| 10    | 47.0%    | 577           | 323               |



### Discussion 

At the start of our project, we noticed a lack of impactful common disease prediction models, as most focused on scope-specific diagnosis. We first built a neural network using source.csv, but its accuracy was only 30%, so we revised our approach. A major challenge was finding consistent datasets, since many had mismatched symptom lists, making tokenization difficult; in the future, large language models (LLMs) like LLAMA could help address this. We also explored transformers and found that using a BERT tokenizer to map symptoms like “Acne” to synonyms improved accuracy to 95%, showing the potential of transformer-based models. While our current model is only a starting point, improvements such as refining TF-IDF calculations, leveraging embeddings, and expanding the dataset could significantly enhance accuracy and reliability in real-world medical applications.

<img width="1189" height="590" alt="countofdis" src="https://github.com/user-attachments/assets/3975cf24-5285-4f5f-b125-00d5071170f6" />
_Caption: The Blue bar is gold label and the yellow bar is the number of accurately predicted label for each unique disease in user input. (Top 10 ranking)
