# Evaluating AI models in health
![health-bow-01](https://user-images.githubusercontent.com/53757856/134309621-0fa65f0a-2310-4f22-aa03-4b0298f12cd6.png)

The ITU/WHO Focus Group on Artificial Intelligence for Health (FG-AI4H) works in partnership with the World Health Organization (WHO) to establish a standardized assessment framework for the evaluation of AI-based methods for health. The group was founded by ITU-T Study Group 16 in 2018.

This repository contains a sample benchmarking configuration that you can base your benchmarks on. Benchmarking is offered in two different versions of submissions: text-based and docker-based. Text-based allows the user/participant to submit the predictions/output of the AI model after evaluation on the provided protected environment with the test dataset and an additional questionnaire filled. These results compared with the ground truths and the general performance of the model evaluation. The additional questionnaire will be analyzed and reviewed by an audit team. Submissions of the predictions/output of the AI model can be made through the user interface (UI), or as an upload or link to the file though the EvalAI command-line interface (CLI). The filled questionnaire can be submitted using the UI of the platform.

For docker-based evaluations, the user/participant submits the AI model to a docker image through the provided EvalAI command line tool. The questionnaire is submitted afterwards through the UI. The AI model will be evaluated in a protected environment with the test dataset. Finally, the audit team will review and make the audit report based on the results obtained.

## How to create a benchmark?

You find a simple configuration as starter kit in this repository that you can replicate to create a benchmark (a.k.a. challenge) on [our platform](https://health.aiaudit.org) in order to assess different ML/AI models. The repository is based on code from (but we are not affiliated to) [EvalAI](https://github.com/cloud-cv/evalai).
Follow the instructions given below to get started. 

## Example text-based benchmark/challenge

The folder retino-public-example contains a fully configured text-based benchmark configuration that we are already hosting on our platform. You can use this example to base your own benchmark on (but for data protection, we have taken
out our annotation and submission files).

## Directory Structure

```
.
├── README.md
├── annotations                                 # Contains the annotations for Dataset splits
│   ├── test_annotations_devsplit.json          # Annotations of dev split
│   └── test_annotations_testsplit.json         # Annotations for test split
├── challenge_data                              # Contains scripts to test the evalautaion script locally
│   ├── challenge_1                             # Contains evaluation script for the challenge
|        ├── __init__.py                        # Imports the main.py file for evaluation
|        └── main.py                            # Challenge evaluation script
│   └── __init__.py                             # Imports the modules which involve evaluation script loading
├── challenge_config.yaml                       # Configuration file to define challenge setup
├── evaluation_script                           # Contains the evaluation script
│   ├── __init__.py                             # Imports the modules that involve annotations loading etc
│   └── main.py                                 # Contains the main `evaluate()` method
├── logo.jpg                                    # Logo image of the challenge
├── submission.json                             # Sample submission file
├── run.sh                                      # Script to create the challenge configuration zip to be uploaded on EvalAI website
└── templates                                   # Contains challenge related HTML templates
    ├── challenge_phase_1_description.html      # Challenge Phase 1 description template
    ├── challenge_phase_2_description.html      # Challenge Phase 2 description template
    ├── description.html                        # Challenge description template
    ├── evaluation_details.html                 # Contains description about how submissions will be evalauted for each challenge phase
    ├── submission_guidelines.html              # Contains information about how to make submissions to the challenge
    └── terms_and_conditions.html               # Contains terms and conditions related to the challenge
├── worker                                      # Contains the scripts to test evaluation script locally
│   ├── __init__.py                             # Imports the module that ionvolves loading evaluation script
│   └── run.py                                  # Contains the code to run the evaluation locally
```


## Create challenge using config

1. Fork this repository.
2. Read the [EvalAI configuration documentation](https://evalai.readthedocs.io/en/latest/configuration.html)
to learn more about how you want to structure your challenge (note that our platform is not affiliated to EvalAI). Once you are ready, start making changes in the yaml file, HTML templates, evaluation script according to your need.
3. Once you are done making changes, run the command `./run.sh` to generate the `challenge_config.zip`.
4. Upload the `challenge_config.zip` on [our platform](https://health.aiaudit.org)
to create a challenge (as mentioned, our platform is not affiliated to EvalAI). The challenge will be available publicly once our admin approves it.
5. To update the challenge, use the UI to update the details.

## Test your evaluation script locally

In order to test the evaluation script locally before uploading it to our server, please follow the below instructions -
1. Copy the evaluation script, i.e, `__init__.py` , `main.py` and other relevant files from `evaluation_script/`
directory to `challenge_data/challenge_1/` directory.
2. Now, edit `challenge_phase` name, `annotation file` name and `submission
file` name in the `worker/run.py` file to the challenge phase codename (which you want to test for), annotation file name in the `annotations/`
folder (for specific phase) and corresponding submission file respectively.
3. Run the command `python -m worker.run` from the directory where `annotations/` `challenge_data/`
and `worker/` directories are present. If the command runs successfully, then the evaluation script works locally and will work on the server as well.

