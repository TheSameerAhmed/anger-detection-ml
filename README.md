# Aggressive Speech Detection :angry:

This repository classifies aggressive speech using supervised machine learning. The data used for classification in this repository comes from a  `in-the-wild` data source, it originates from a subreddit: `/r/publicfreakout`. The repository contains several Jupyter notebooks that do modelling, clustering, calculating inter onserver error (IOE) and visualizing of the data respectively. Additonally, the repository also contains dataset files such that all the Jupyter notebooks can run directly by simply cloning this repository.

## Structure of the repository  :file_folder: :file_folder:

1. [CleanData](CleanData) contains all the dataset files that have been aligned such that they all have an identical syntax.
2. [extracted](extracted) contains all dataset files that have been segregated such that they only contain the feature values. Moreover, it also contains a single dataset file that merges all the collected data and puts it into a single `.csv` file: [extracted/full-train-features](extracted/full-train-features). 
3. Our primary codebase for all the classification modelling lies completely in the [modelling/modelling.ipynb](modelling/modelling.ipynb)
4. [clustering.ipynb](clustering.ipynb) contains code to ensure that we can move ahead with our chosen 4 labels such that their is a natural grouping for all 4 labels.
5. [IOE_script.ipynb](IOE_script.ipynb) calculates the inter observer error of our data as the name implies. [remove_invalid.ipynb](remove_invalid.ipynb) creates the `cleaned-data` which is consequenetly stored in [CleanData](CleanData)
6. [visualizations.ipynb](visualizations.ipynb) helps to determine the relavant feature set for our machine learning models. :bar_chart:
7. Lastly, the [voice_toolbox](voice_toolbox) contains all the code used in this project to extract the features from the audio files.

 <details>

 <summary>ML Algortihms used in the Jupyter Notebooks</summary>

| Jupyte Notebook      | Running time*  |
| -------------------- | -------------- |
| clustering.ipynb     | Principal Componenet Analysis, KMeans       |
| modelling.ipynb      |  Supoprt Vector Machines, Decision Tree, Random Forest, XG Boost, Gradient Boost, k-nearest neighbors, Adaptive Boosting     |
| IOE_script.ipynb     |    Cohen Kappa |


 </details>

## Structure of the data :bar_chart:

- Labelling of the audio files is based on the labels below:
    - 0 = no aggression
    - 1 = annoyance
    - 2 = threatening (encroaching on aggression)
    - 3 = aggression (causes fear or caution)
- Participants were made to label the data based on what they perceived to be the most accurate label for a particular audio file.
- As our data comes from `in-the-wild` we also included a `noisy` binary value for participants to denote the following:
    - 0 = can clearly distinguish how many voices are present
    - 1 = many voices that can not be distinguishes
- **Therefore, in many parts of our various Jupyter Notebooks you will encounter `Groups`. These groups are defined based on the following distinctions:**
    - Group 1 : all data for both noisy = 1 and noisy = 0
    - Group 2 : non noisy data for when noisy = 0
    - Group 3 : noisy data for when noisy = 1
- The above distinction between the groups was done primarily to explore potential hidden patters that could aid us to devise a more robust classifciation model.
- Lastly, our collected audio files from the subreddit are of varying lengths because of the inherent nature of in-the-wild data. Therefore, a particular `parent` audio file has been further divided into 10 second `segments` of the parent file.
- Participants were made to label only segment files as `segment_label` and the maximum `segment_label` was annotated to the `parent_label`.
- **Consequently, in many parts of our Notebooks you will notice analysis being done on both `parent` and `segment`. Once again, this was done to achieve a more robust classification model.**  


## Instructions to run code :running: :running:

1. All our Jupyter Notebooks (except remove_invalid.ipynb) have been designed such that the notebooks can simply be run by a `Run All` command in your respective IDEs to run all the code blocks sequentially.
2. [modelling/modelling.ipynb](modelling/modelling.ipynb) should be run if you are solely interested in our final classification model.
3. Various packages can either be installed by running the very first `Install Packages` code block by **uncommenting** the code in those code cells.
4. Alternatively, the packages can also be installed by the following command given `pip` is already installed in the machine running the code:
```
pip install -r requriements.txt
```

 <details>

 <summary><strong>Running times for the Jupyter Notebooks</strong></summary>
  
| Jupyte Notebook      | Running time*                                      |
| -------------------- | -------------------------------------------------- |
| clustering.ipynb     |    ~ 10s                                           |
| modelling.ipynb      |    ~ 120s                                          |
| IOE_script.ipynb     |    ~ 60s                                           |
| visualizations.ipynb |    ~ 50s                                           |
| remove_invalid.ipynb | cannot be run (read special considerations below)  |

*time does not include time taken to install packages i.e. runing the `Installing Packages` code block

</details>


## Special Considerations

1. The `remove_invalid.ipynb` notebook cannot be run by simply cloning this repo.
    - Since, this notebook looks to remove audio files from our dataset that have a low agreement in terms of labelling between our participants. Due to size limitations imposed on GitHub repositories we cannot upload all our data (audio files worth `10GB`+ in total)
2. `modelling.ipynb` contains certain hyperparameter tuning code blocks that have been intentionally commented out. This is done so that the notebook can be run within a reasonable amount of time. 
    - Not commenting those hyperparameter tuning code block leads the total time taken to run the notebook to over 8 hours.
3. Radar plot in `visualizations.ipynb` require a cerain version of plotly or else the packages run into a dependency problem. We recommend uncommenting the code block in `visualizations.ipynb` to `Install Packages`, particularly the last comment in that code. 
    - Alternatively, you can run the following `pip` command to ensure there are no problems with the `plotly` version:
    ```
    pip install --upgrade nbformat
    ```


## Self-evaluation of our project

We were able to do most of what we had planned to based on our project proposal such as the following:
- Extracting a comprehensive feature set from our audio files. Code for which can be found under the [voice_toolbox](voice_toolbox) folder of this repository.
- Calculating Inter observer error to arrive at more accurate labelling of our data. Code for which can be found in [IOE_script.ipynb](IOE_script.ipynb).
- Clustering using Principal Componenet Analysis and KMeans. Code for which can be found in [clustering.ipynb](clustering.ipynb).
- Classification using SVM was proposed and was successfully completed. Moreover, we eventually decided to do an Ensemble learning which meant that we had to run various Machine Learning Algorithms such as Decision Tree, Random Forest, XG Boost, Gradient Boost, k-nearest neighbors and Adaptive Boosting.  Ensemble learning was not anticipated when we had drafted our proposal. Code for all of which can be found in [modelling/modelling.ipynb](modelling/modelling.ipynb).
- Furthermore, we conducted a lot of Exploratory Data Analysis (EDA) to arrive at the best possible classification model. Once again, code for our EDA can be found in [modelling/modelling.ipynb](modelling/modelling.ipynb). We also conducted an anova test that has been written in R, which can be found in [affective-anova.rmd](affective-anova.rmd).
