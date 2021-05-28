# Day 2 - Afternoon (1:30 PM - 5:00 PM)

**What we cover**
* Recurrent Neural Network
* Long Short Term Memory to predict a sine function

:pencil2: Lecture slide (Day2PM-1) - TBU

:pencil2: Lecture slide (Day2PM-2) - TBU


### Assignment #2 : Image classification (CIFAR10) ###

__CIFAR-10 with MLP and CNN__

<img src="https://github.com/isaacyeSN/SS2021/blob/main/Day2PM/cifar-10.png" width="450" height="300"/>

:computer:: [[start-up code]](https://github.com/isaacyeSN/SS2021/blob/main/Day2PM/SS21Day2PM_Assignment.ipynb)

:computer:: [[start-up code (full)]] - TBU

---

:computer:: Lab 6 [[start-up code]](https://github.com/isaacyeSN/SS2021/blob/main/Day2PM/SS21Day2PM_Lab6_LSTM.ipynb)

:computer:: Lab 6 (Sine Function + LSTM) [[start-up code (full)]] - TBU

---
## Setting up virtual environment in Graham

Virtual Environment(VE) supported by Python is a working place only for your work, so you can add/delete any packages you need. Here we practice to install necessary packages for ML framework - PyTorch. 

To create a VE on the clusters do the following:
```
module load StdEnv/2020
module load python/3.8.2
module load scipy-stack/2020b
virtualenv --no-download ~/VENV
```
As you may guess, **VENV** is the name of the virtual environment. (You can choose whatever you want)

You can activate your VE by

```
source ~/VENV/bin/activate
```
and deactivate it by typing the command below in the VE

```
deactivate
```

Once it is activated, you can see the command prompt in your terminal changed as follows.

![virtualenv3](https://github.com/isaacye/SS2021/blob/main/Day1AM/ve3.png)

Before installing any packages (modules), you better check if your **pip** (python package manager) is up to date. (Note that it is done once after activating **VE**.)

```
pip install --upgrade pip
```

Now, we need to install PyTorch packages by checking our **wheelhouse**.  
(Note that PyTorch is named as *torch* in our wheelhouse.)

```
avail_wheels torch
```

![virtualenv4](https://github.com/isaacye/SS2021/blob/main/Day1AM/ve4.png)

If you type __avail_whees__, you will have the full list of available wheels in the system. For information on how to search for things like specific versions, see the wiki [here](https://docs.computecanada.ca/wiki/Python#Available_wheels).

To install PyTorch, just type:

```
pip install --no-index torch
```

The portion of this command that specifies the local wheelhouse install is "--no-index". If this is not present, pip will attempt to download the wheel from the internet. 

Once it's successfully installed, you can check by 

```
pip list | grep torch
```


![virtualenv5](https://github.com/isaacye/SS2021/blob/main/Day1AM/ve5.png)

Run Python in the VE to start the interpreter as follows

```python```

and import torch to see if it works fine:

```
import torch
print(torch.__version__)
```

![virtualenv6](https://github.com/isaacye/SS2021/blob/main/Day1AM/ve6.png)

---

#### Running a DL code on `_interactively_` in Graham ####

1. Make a directory and upload your source code into it.

    ```
   cd /home/$USER
   mkdir /home/$USER/scratch/$USER/ML
   ```
   

2. Start interactive running mode with CPU/GPU in Graham 
   
   **For CPU**:
   
   ```
    salloc --time=0:30:0 --ntasks=1 --cpus-per-task=3 --mem=1000M --account=def-training-wa_cpu --reservation=snss-wr_gpu 
   ```

   **For GPU**:
   
   ```
    salloc --time=0:30:0 --ntasks=2 --gres=gpu:2 --cpus-per-task=3 --mem=1000M --account=def-training-wa_gpu --reservation=snss-wr_gpu 
   ```

3. virtual environment (make sure you load python and scipy-stack module)

    ```
    module load python
    module load scipy-stack
    source ~/ENV/bin/activate
    ```

4. Run it 
    ```
    python SS20_lab3_LR_MLPg.py
    ```
    
#### Running a DL code `_via scheduler_` in Graham ####

1.  Write a submission script 'job_s.sh' like below using text editor  
    ```
    #!/bin/bash
    #
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=2
    #SBATCH --cpus-per-task=3
    #SBATCH --gres=gpu:t4:2
    #SBATCH --mem=20000M
    #SBATCH --time=0-30:00
    #SBATCH --account=def-training-wa_gpu
    #SBATCH --reservation=snss_wr_gpu
    #SBATCH --output=slurm.%x.%j.out
    
    module load python scipy-stack
    source ~/ENV/bin/activate
    cd /home/$USER/scratch/$USER/ML
    python /home/$USER/scratch/$USER/ML/YOUR-PYTHONCODE-NAME.py
    
    ```
    
4. Submit it
    ```
    sbatch job_s.sh
    ```

5. Check the submitted job
    ```
    squeue -u $USER
    ```
You can find more information at [Compute Canada wiki](https://docs.computecanada.ca/wiki/Running_jobs)
