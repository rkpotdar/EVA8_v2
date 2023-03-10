# ADVANCED TRAINING CONCEPTS
Objective is to learn Class activation maps, Weight Updates, Optimizers & LR Schedulers concepts. And to perform a customized convolution based on ResNet18, Layer Normalization on CIFAR10 dataset. 

## Vision Library
Fully modularized library - [torch_cv_wrapper](https://github.com/rkpotdar/torch_cv_wrapper) is built to perform object detection based on PyTorch on CIFAR10 dataset.

**Folder Structure**

    |── config
    |   ├── config.yaml    
    ├── dataloader  
    |   ├── albumentation.py 
    |   ├── load_data.py
    ├── model  
    |   ├── custommodel.py 
    |   ├── resnet.py
    ├── utils  
    |   ├── __init__.py 
    |   ├── train.py 
    |   ├── test.py 
    |   ├── plot_metrics.py 
    |   ├── helper.py 
    |   ├── gradcam.py 
    ├── main.py     
    ├── README.md  

### Final Model details

Epochs - 40 <br>
Normalization - LayerNorm <br>
LR Scheduler - ReduceLROnPlateau

Following Data Augmentation is applied, refer [this](https://github.com/rkpotdar/torch_cv_wrapper/blob/master/dataloader/albumentation.py) 
- RandomCrop(32, padding=4)
- CutOut(16x16)
- Rotate(±5°)

The final notebook is [here](https://github.com/rkpotdar/EVA8_v2/blob/master/CIFAR10_Image_Classification_Resnet18.ipynb) with a test accuracy of 90% at 39th epoch and code for individual experiments can be found [here](https://github.com/gkdivya/EVA/tree/main/8_AdvancedTrainingConcepts/experiments)

### Experiments
| ResNet Model | Normalization       | Scheduler         | Params | Training Accuracy | Test Accuracy | Experiment Files                                                                                                                                                |
| ------------ | ------------------- | ----------------- | ------ | ----------------- | ------------- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ResNet18     | Batch Normalization | OneCycleLR       |   11,173,962     |   97.51%               |     93.79%           | [ResNet18_BatchNormalization_OneCycleLR](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet18_BN_OneCycleLR)                       |
| ResNet18     | Batch Normalization | LRScheduler       |  11,173,962      |    95.44%               |    92.84%           | [ResNet18_BatchNormalization_LRScheduler](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet18_BN_LR)                              |
| ResNet18     | Batch Normalization | ReduceLROnPlateau |   11,173,962     |     95.79%                |       92.72%          | [ResNet18_BatchNormalization_ReduceLROnPlateau](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet18_BN_RedLR)                     |
| ResNet18     | Layer Normalization | OnceCycleLR       |   11,173,962     |   94.88%                 |  92.00%              | [ResNet18_LayerNormalization_OneCycleLR](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet18_LN_OneCycleLR)                       |
| ResNet18     | Layer Normalization | LRScheduler       |  11,173,962      |   91.16%        |   89.77%           | [ResNet18_LayerNormalization_LRScheduler](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet18_LN_LR)                              |
| ResNet18     | Layer Normalization | ReduceLROnPlateau |  11,173,962      |      94.94%             |     91.7%          | [ResNet18_LayerNormalization_ReduceLROnPlateau](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet18_LN_RedLR)                     |
| ResNet34     | Batch Normalization | OnceCycleLR       | 21,282,122       |   97.47%        |        94.52%       | [ResNet34_BatchNormalization_OneCycleLR](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet34_BN_OneCycleLR)                       |
| ResNet34     | Batch Normalization | LRScheduler       |  21,282,122      |    94.09%     |     92.10%           | [ResNet34_BatchNormalization_LRScheduler](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet34_BN_LR)                              |
| ResNet34     | Batch Normalization | ReduceLROnPlateau | 21,282,122        |     94.14%              | 92.39%              | [ResNet34_BatchNormalization_ReduceLROnPlateau](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet34_BN_RedLR)                     |
| ResNet34     | Layer Normalization | OnceCycleLR       |  21,282,122       |        95%           |     92.02%          | [ResNet34_LayerNormalization_OneCycleLR](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet34_LN_OneCycleLR)                       |
| ResNet34     | Layer Normalization | LRScheduler       | 21,282,122         |       87.25%            |  88.54%             | [ResNet34_LayerNormalization_LRScheduler](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet34_LN_LR)          |
| ResNet34     | Layer Normalization | ReduceLROnPlateau | 21,282,122        |          81.40%         |      84.47%         | [ResNet34_LayerNormalization_ReduceLROnPlateau](https://github.com/rkpotdar/EVA8_v2/blob/master/experiments/Cifar10_with_resnet34_LN_RedLR) |


### Training and Testing Logs

    Epoch 1:
    Loss=1.8958317041397095 Batch_id=195 LR=0.00100 Accuracy=20.26: 100%|██████████| 196/196 [00:58<00:00,  3.35it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0077, Accuracy: 2779/10000 (27.79%)

    Epoch 2:
    Loss=1.7341811656951904 Batch_id=195 LR=0.00100 Accuracy=31.44: 100%|██████████| 196/196 [00:58<00:00,  3.35it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0066, Accuracy: 3977/10000 (39.77%)

    Epoch 3:
    Loss=1.5829461812973022 Batch_id=195 LR=0.00100 Accuracy=38.97: 100%|██████████| 196/196 [00:58<00:00,  3.35it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0060, Accuracy: 4445/10000 (44.45%)

    Epoch 4:
    Loss=1.419417142868042 Batch_id=195 LR=0.00100 Accuracy=42.76: 100%|██████████| 196/196 [00:58<00:00,  3.36it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0056, Accuracy: 4971/10000 (49.71%)

    Epoch 5:
    Loss=1.5358864068984985 Batch_id=195 LR=0.00100 Accuracy=47.01: 100%|██████████| 196/196 [00:58<00:00,  3.35it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0056, Accuracy: 4981/10000 (49.81%)

    Epoch 6:
    Loss=1.4621860980987549 Batch_id=195 LR=0.00100 Accuracy=50.62: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0049, Accuracy: 5483/10000 (54.83%)

    Epoch 7:
    Loss=1.156994104385376 Batch_id=195 LR=0.00100 Accuracy=54.02: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0043, Accuracy: 5959/10000 (59.59%)

    Epoch 8:
    Loss=0.917637825012207 Batch_id=195 LR=0.00100 Accuracy=56.78: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0050, Accuracy: 5435/10000 (54.35%)

    Epoch 9:
    Loss=1.1820430755615234 Batch_id=195 LR=0.00100 Accuracy=58.46: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0039, Accuracy: 6552/10000 (65.52%)

    Epoch 10:
    Loss=1.093083143234253 Batch_id=195 LR=0.00100 Accuracy=61.01: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0040, Accuracy: 6408/10000 (64.08%)

    Epoch 11:
    Loss=1.14859938621521 Batch_id=195 LR=0.00100 Accuracy=63.37: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0036, Accuracy: 6854/10000 (68.54%)

    Epoch 12:
    Loss=0.9431864023208618 Batch_id=195 LR=0.00100 Accuracy=65.24: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0035, Accuracy: 6900/10000 (69.00%)

    Epoch 13:
    Loss=0.9380429983139038 Batch_id=195 LR=0.00100 Accuracy=67.04: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0036, Accuracy: 6861/10000 (68.61%)

    Epoch 14:
    Loss=0.7487483024597168 Batch_id=195 LR=0.00100 Accuracy=69.01: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0031, Accuracy: 7207/10000 (72.07%)

    Epoch 15:
    Loss=0.8383620977401733 Batch_id=195 LR=0.00100 Accuracy=70.26: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0028, Accuracy: 7507/10000 (75.07%)

    Epoch 16:
    Loss=0.917985737323761 Batch_id=195 LR=0.00100 Accuracy=72.14: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0027, Accuracy: 7622/10000 (76.22%)

    Epoch 17:
    Loss=0.7565293312072754 Batch_id=195 LR=0.00100 Accuracy=73.48: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0024, Accuracy: 7931/10000 (79.31%)

    Epoch 18:
    Loss=0.6109765768051147 Batch_id=195 LR=0.00100 Accuracy=74.51: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0026, Accuracy: 7780/10000 (77.80%)

    Epoch 19:
    Loss=0.7406558394432068 Batch_id=195 LR=0.00100 Accuracy=75.73: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0023, Accuracy: 7989/10000 (79.89%)

    Epoch 20:
    Loss=0.651975154876709 Batch_id=195 LR=0.00100 Accuracy=77.06: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0022, Accuracy: 8093/10000 (80.93%)

    Epoch 21:
    Loss=0.8543360829353333 Batch_id=195 LR=0.00100 Accuracy=78.22: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0022, Accuracy: 8131/10000 (81.31%)

    Epoch 22:
    Loss=0.5843213200569153 Batch_id=195 LR=0.00100 Accuracy=78.30: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0023, Accuracy: 8041/10000 (80.41%)

    Epoch 23:
    Loss=0.7562752962112427 Batch_id=195 LR=0.00100 Accuracy=79.49: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0019, Accuracy: 8379/10000 (83.79%)

    Epoch 24:
    Loss=0.40172165632247925 Batch_id=195 LR=0.00100 Accuracy=80.36: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0019, Accuracy: 8360/10000 (83.60%)

    Epoch 25:
    Loss=0.5321276783943176 Batch_id=195 LR=0.00100 Accuracy=80.74: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0019, Accuracy: 8434/10000 (84.34%)

    Epoch 26:
    Loss=0.5310409665107727 Batch_id=195 LR=0.00100 Accuracy=81.55: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0018, Accuracy: 8430/10000 (84.30%)

    Epoch 27:
    Loss=0.5504230260848999 Batch_id=195 LR=0.00100 Accuracy=82.20: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0018, Accuracy: 8466/10000 (84.66%)

    Epoch 28:
    Loss=0.4548879563808441 Batch_id=195 LR=0.00100 Accuracy=82.94: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0019, Accuracy: 8371/10000 (83.71%)

    Epoch 29:
    Loss=0.38220348954200745 Batch_id=195 LR=0.00100 Accuracy=83.10: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0017, Accuracy: 8550/10000 (85.50%)

    Epoch 30:
    Loss=0.5645345449447632 Batch_id=195 LR=0.00100 Accuracy=83.33: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0015, Accuracy: 8732/10000 (87.32%)

    Epoch 31:
    Loss=0.4112061560153961 Batch_id=195 LR=0.00100 Accuracy=84.24: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0016, Accuracy: 8664/10000 (86.64%)

    Epoch 32:
    Loss=0.5791297554969788 Batch_id=195 LR=0.00100 Accuracy=84.57: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0015, Accuracy: 8705/10000 (87.05%)

    Epoch 33:
    Loss=0.3664173185825348 Batch_id=195 LR=0.00100 Accuracy=85.09: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0017, Accuracy: 8615/10000 (86.15%)

    Epoch 34:
    Loss=0.1975061595439911 Batch_id=195 LR=0.00100 Accuracy=85.18: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0015, Accuracy: 8790/10000 (87.90%)

    Epoch 35:
    Loss=0.3392057418823242 Batch_id=195 LR=0.00100 Accuracy=85.38: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0016, Accuracy: 8690/10000 (86.90%)

    Epoch 36:
    Loss=0.4261108338832855 Batch_id=195 LR=0.00100 Accuracy=85.83: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0016, Accuracy: 8689/10000 (86.89%)

    Epoch 37:
    Loss=0.30360835790634155 Batch_id=195 LR=0.00100 Accuracy=86.37: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0015, Accuracy: 8782/10000 (87.82%)

    Epoch 38:
    Loss=0.5165297389030457 Batch_id=195 LR=0.00100 Accuracy=86.28: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0016, Accuracy: 8728/10000 (87.28%)

    Epoch    38: reducing learning rate of group 0 to 2.0000e-04.
    Epoch 39:
    Loss=0.12279750406742096 Batch_id=195 LR=0.00020 Accuracy=89.82: 100%|██████████| 196/196 [00:58<00:00,  3.34it/s]
      0%|          | 0/196 [00:00<?, ?it/s]
    Test set: Average loss: 0.0013, Accuracy: 9009/10000 (90.09%)

    Epoch 40:
    Loss=0.1579943150281906 Batch_id=195 LR=0.00020 Accuracy=91.21: 100%|██████████| 196/196 [00:58<00:00,  3.33it/s]
    Test set: Average loss: 0.0013, Accuracy: 8975/10000 (89.75%)



### Loss and Accuracy Plots

![image](https://user-images.githubusercontent.com/42609155/124164963-ec6add80-dabe-11eb-8b5f-43a9f93e866c.png)


### Confusion Matrix and Accuracy by class

    Accuracy of plane : 90 %
    Accuracy of   car : 93 %
    Accuracy of  bird : 82 %
    Accuracy of   cat : 77 %
    Accuracy of  deer : 91 %
    Accuracy of   dog : 87 %
    Accuracy of  frog : 93 %
    Accuracy of horse : 91 %
    Accuracy of  ship : 95 %
    Accuracy of truck : 93 %

![image](https://user-images.githubusercontent.com/42609155/124165043-086e7f00-dabf-11eb-8804-345898d1c573.png)

### Misclassified Images

20 missclassified images


![image](https://user-images.githubusercontent.com/42609155/124165004-fb519000-dabe-11eb-855b-7c85ece69c0e.png)

### Model diagnostic with Grad-CAM

Gradcam output for the above 20 missclassified images

![image](https://user-images.githubusercontent.com/42609155/124165243-2c31c500-dabf-11eb-9f0e-cdf08d0e605d.png)

![image](https://user-images.githubusercontent.com/42609155/124165318-3fdd2b80-dabf-11eb-92fc-dab30334e2c6.png)

### Tensorboard Logs
![image](https://user-images.githubusercontent.com/17870236/124290030-93f41880-db70-11eb-9a3a-bfe05b08346c.png)



