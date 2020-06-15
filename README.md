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
sys.path.insert(0, os.path.abspath('/opt/intel'))</pre></code>
