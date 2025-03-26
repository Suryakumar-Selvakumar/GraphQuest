# GraphQuest: Unveiling Player Engagement in Multiplayer Games

This is my **Course Project**, aligned with the course - **Data Science**, and associated with my **Master's Degree in Computer Science** at the **University of Colorado Denver**.

## Project Description

<div style="text-align: justify">
Online gaming has become an entertainment staple in the modern world, with an estimated market value of 96 Billion Dollars. The industry is forecasted to grow exponentially over the coming years with a predicted market value of 276 Billion Dollars by 2033. This rapid rise of online gaming would soon place it at the very top in the entertainment industry, well above others such as the Film & Music industries in terms of market value. With such global prevalence and potential for profits, it is becoming increasingly important for Gaming companies to understand the online gaming demographic, what drives their engagement levels, and what incentivizes them to make in-game purchases. This project aims to perform a comprehensive data analysis of a dataset that includes player demographics & statistics across different genres of online games, train a highly accurate XGBoost Classifier on the dataset to predict the engagement level of players, yield valuable insights, and provide actionable
suggestions to Gaming companies to maximize player engagement and in-game purchases.
</div>

## Instructions to Run the Project

**1. Fork & Clone the repo:** <br>
`git clone https://github.com/your-username/your-forked-repo.git`

**2. Download the final model from this Drive [Link](https://drive.google.com/file/d/1zgrXH_bxOSE21FbVnyZGK0MxgjI4w8nT/view?usp=sharing)**

- The size of the model is around `105MB`. Since this exceeds git's limit of `100MB` per file, I chose to save the model in Google Drive.
- Once downloaded, place the `final_xgboost_model.pkl` file inside the `models` folder.
- The model should be accessible in the notebooks.

**3. Create a virtual env with Conda and Install all required dependencies:**

_Approach #1: Use provided `environment.yml`_

- `conda env create -f environment.yml`
- Activate conda env with `conda activate graphquest`
- It is highly recommended to run this project on a Linux system. If that is not an option, please follow Approach #2.

_Approach #2: Use provided `requirements.txt`_

- `conda create -n your-env-name python=3.9`
- `conda activate your-env-name`
- `pip install -r requirements.txt`
- OS-specific Conda libraries that may be needed for the project may have to be installed manually.

**4. Steps to run the project files:**

- Create an ipykernel with your conda env using `python -m ipykernel install --user --name=graphquest`
- Now, use `jupyter notebook` command to launch the jupyter notebook server, from which the user can run the notebooks. Make sure to switch to `graphquest` kernel before running the code.
- Alternatively, the user can run the notebooks in VSCode or any Code Editor that allows to do so.

**5. The primary model used in this project is the XGBoost Classifier which takes full advantage of an Nvidia GPU's computing power facilitated by the CUDA API. Hence, run times for the notebooks may vary depending on your GPU. Below is the GPU config that was used to build the project:**

- GPU: _NVIDIA GeForce RTX 4070 Ti_
- Driver Version: _550.144.03_
- CUDA Version: _12.4_

**6. CUDA versions upto 12.7 are compatible with XGBoost 2.1.3 (The env version). There are two ways the user may install the CUDA module needed for the project:**

_Approach #1: Use conda_

- Activate conda env with `conda activate graphquest`
- Install the CUDA toolkit using `conda install -c nvidia cuda-toolkit=12.4.0`
- Type `nvcc --version` to verify the CUDA version 

_Approach #2: Download the CUDA module globally and make conda env point to it_

- Find and Download the preferred CUDA version in this [archive](https://developer.nvidia.com/cuda-toolkit-archive)
- Install the library and verify installation using `nvcc --version`
- If the command does not return the expected CUDA version,
    - Open shell config file using `nano ~/.bashrc`
    - Look for the lines `export PATH=/usr/local/cuda-12.4/bin:$PATH` and `export LD_LIBRARY_PATH=/usr/local/cuda-12.4/lib64:$LD_LIBRARY_PATH`
    - If they are missing, add them to the config
    - Save using `source ~/.bashrc`
    - Test the global path using `echo $PATH` and ensure it points to the correct CUDA version and it's bin folder. For example, `/usr/local/cuda-12.4/bin`
    - Re-verify using `nvcc --version`
- Activate Conda env and test using `nvcc --version` to check if it correctly points to the expected CUDA
- If it does not, follow these steps to create an activation script:
    - Create the script using `mkdir -p ~/anaconda3/envs/graphquest/etc/conda/activate.d`
    - Access it with `nano ~/anaconda3/envs/graphquest/etc/conda/activate.d/env_vars.sh`
    - Add the `export` paths mentioned above to this file as well.
    - Save file and Reactivate conda env
    - Check again using `nvcc --version`

_Upon completion of either approach, ensure GPU compatibility by running Line 3 in the `Model Training & Evaluation` notebook which should return "GPU is available: True"_ 

**7. The code in the notebook `Model Training & Evaluation` is setup in such a way that new models won't be trained and new SHAP values won't get generated if those models or the values already exist locally. If the user wishes to train any of the models themselves or regenerate the SHAP values, ensure to delete or rename or move the respective pre-existing files.**

**8. File-Specific Information:**
- _`Notebook-1 – Exploratory Data Analysis`_: Contains Statistical Summaries, Visualizations, and Interpretion of the Results, including Stakeholder Recommendations for the "Predict Online Gaming Behavior Dataset". Run time was relatively low on my system, ~5 minutes.
- _`Notebook-2 – Dataset Pre-processing`:_ Feature Engineering and Encoding of Categorical data in the dataset was done in this notebook. Fast runtime, likely less than 2 minutes.
- _`Notebook-3 – Model Training and Evaluation`:_ The run-time performance of the GPU-accelerated XGBoost Classifer heavily depends on the user's GPU. Therefore, the time taken for the training of Baseline & Final models, Optuna Study trials, and 10-Fold Cross-Validation are all dependent on the same. Stronger the GPU, faster the run time. It took around 10 minutes on my GPU.