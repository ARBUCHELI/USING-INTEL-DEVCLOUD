# USING-INTEL-DEVCLOUD

## This Content was Created by Intel Edge AI for IoT Developers UDACITY Nanodegree.

This notebook is a demonstration showing you how to request an edge node with an Intel i5 CPU and load a model on the CPU using Udacity's 
workspace integration with Intel's DevCloud. This notebook is just to give you an overview of the process (you won't be writing any code).
In the next workspace, you'll be given TODO items to complete.

Below are the six steps we'll walk through in this notebook:

1. Creating a Python script to load the model
2. Creating a job submission script
3. Submitting a job using the qsub command
4. Checking the job status using the liveQStat function
5. Retrieving the output files using the getResults function
6. View the resulting output

Click the <strong>Introduction to DevCloud</strong> button below for a quick overview of the overall process. We'll then walk through each step of the process.

<strong>IMPORTANT: Set up paths so we can run Dev Cloud utilities</strong>

You must run this every time you enter a Workspace session.

<pre><code>%env PATH=/opt/conda/bin:/opt/spark-2.4.3-bin-hadoop2.7/bin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/intel_devcloud_support
import os
import sys
sys.path.insert(0, os.path.abspath('/opt/intel_devcloud_support'))
sys.path.insert(0, os.path.abspath('/opt/intel'))</code></pre>

# The Model
We will be using the <pre><code>vehicle-license-plate-detection-barrier-0106</code></pre> model for this exercise. Remember that to run a model on the CPU, we need to use <pre><code>FP32</code></pre> as the model precision.

The model has already been downloaded for you in the <pre><code>/data/models/intel</code></pre> directory on Intel's DevCloud. We will be using the following filepath during the job submission in <strong>Step 3:</strong>

<strong>/data/models/intel/vehicle-license-plate-detection-barrier-0106/FP32/vehicle-license-plate-detection-barrier-0106</strong>

# Step 1: Creating a Python Script
The first step is to create a Python script that you can use to load the model and perform an inference. I have used the <code>%%writefile</code> magic command to create a Python file called <code>load_model.py</code>.

This will create a new Python file in the working directory.

<pre><code>%%writefile load_model.py

import time
from openvino.inference_engine import IENetwork
from openvino.inference_engine import IECore
import argparse

def main(args):
    model=args.model_path
    model_weights=model+'.bin'
    model_structure=model+'.xml'
    
    start=time.time()
    model=IENetwork(model_structure, model_weights)

    core = IECore()
    net = core.load_network(network=model, device_name='CPU', num_requests=1)

    print(f"Time taken to load model = {time.time()-start} seconds")

if __name__=='__main__':
    parser=argparse.ArgumentParser()
    parser.add_argument('--model_path', required=True)
    
    args=parser.parse_args() 
    main(args)</code</pre>
