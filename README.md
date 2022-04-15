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

## Structure of the data

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
- **Consequently, in many parts of our N
otebooks you will notice analysis being done on both `parent` and `segment`. Once again, this was done to achieve a more robust classification model.**  

## Instructions to run code

1. All our Jupyter Notebooks have been designed such that the notebooks can simply be run by a `Run All` command in your respective IDEs to run all the code blocks sequentially.
2. Various packages can either be installed by running the very first `Installing Packages` by uncommenting the code in those code cells.
3. Alternatively, the packages can also be installed by the following command given pip is already installed in the machine running the code:
```
pip install -r requriements.txt
```

 <details>

 <summary><strong>Running times for the Jupyter Notebooks</strong></summary>
  
| Jupyte Notebook      | Running time* |
| -------------------- | ------------  |
| clustering.ipynb     |    ~ 10s      |
| Paragraph   | Text        |

*time does not include time taken to install packages i.e. runing the `Installing Packages` code block