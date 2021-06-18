<h1>Machine Learning Operations (MLOps) Notes</h1>
<b>Prepared by Vytautas Bielinskas.</b>

<h2>The MLOps Lifecycle</h2>
<p><ul>
  <li><b>ML development</b> concerns experimenting and developing a robust and reproducible model training procedure (training pipeline code), which consists of multiple tasks from data preparation and transformation to model training and evaluation.</li>
  <li><b>Training operationalization</b> concerns automating thre process of packaging, testing, and deploying repeatable and reliable training pipelines.</li>
  <li><b>Continuous training</b> concerns repeatedly executing the training pipeline in response to the new data or to code changes, or on a schedule, potentially with new training settings.</li>
  <li><b>Model deployment</b> concerns packaging, testing, and deploying a model to a serving environment for online experimentation and production serving.</li>
  <li><b>Prediction serving</b> is about serving the model that is deployed in production for inference.</li>
  <li><b>Continuous monitoring</b> is about monitoring the effectiveness and efficiency of a deployed model.</li>
  <li><b>Data and model management</b> is a central, cross-cutting functon for governing ML artifacts to support audit-ability, traceability, and compliance. Data and model management can also promote shareability, resuability, and discoverability of ML assets</li>
  </ul></p>
  
<h2>MLOps Workflow</h2>
<p>The MLOps Workflow is segmented into two modules:
<ul>
  <li><b>MLOps pipelines</b> (build, deploy, and monitoring) - the upper layer.</li>
  <ul style=list-style-type: circle>
  <li style=square><b>Build</b> pipeline: Data ingestion, Model training, Model testing, Model packaging, Model registering.</li>
    <ul style=list-style-type: circle>
      <li>
      <b>Data ingestion</b>: This step is a trigger step of the ML Pipeline. It deals with the volume, velocity, veracity, and variety of data by extracting data from various data sources and ingesting the required data for the model training step. Robust data pipelines connected to multiple data sources enable it to perform <b>ETL</b> operations to provide necessary data for ML training purposes.
      </li>
      <li>
      <b>Model training</b>: After procuring the required data for ML model training, this step will enable model training. It has modular scripts or code that performs all he traditional steps in ML, such as data pre-processing, feature engineering, and feature scaling before training or retraining any model. <b>Grid Search</b> or <b>Random Search</b> cam be used for automatic hyperparameter tuning.
    </li> 
      <li>
      <b>Model testing</b>: In this tep, we evaluate the trained model performance on a separated set of data points named <b>test data</b> - which was split and versioned in <i>Data ingestion</i> step. The inference of the trained model is evaluated according to selected metrics as per the use case. The output of this step is a report on the trained model's performance.
    </li>  
      <li>
      <b>Model packaging</b>: After trained model has been tested in the previous step, the model can be serialized into a file or containerized (using <i>Docker</i>) to be exported to the production environment.
    </li> 
      <li>
      <b>Model registering</b>: The model that was serialized or containerized is registered and stored in the model registry. A registered model is a logical collection of package of one or more files that assemble, represent, and execute your ML model. For example, multiple files can be registered as one model. For instance, a classification model can be comprised of a vectorizer, model weights, and serialized model files. All these files can be registered as one single model. After registering the model, the model can be downloaded and deployed as needed.
    </li> 
  </ul>
  <li style=square><b>Deploy</b>. The deploy module enables operationalizing the ML models we developed in <i>build</i> stage. Deploy pipeline consist of two major components: <b>Application Testing</b> which transforms into <b>Production Release</b>. Deployment pipeline is enabled by streamlined CI/CD pipelines connecting the development to production environments.</li>
    <ul style=list-style-type: circle>
      <li>
      <b>Application testing</b>: Before deploying an ML model to production, it is vital to test its robustness and performance via testing. So, for this we have <i>Application testing</i> phase where we need to test all the trained models for robustness and performance in a production-like environment alled a <b>test environment</b>. This environment must replicate the production environment.<br>
        The ML model for testing is deployed as an API or streaming service in the test environment to deployment targets such as <b>Kubernetes</b> clusters, container instances, or scalable virtual machines or edge devices as per the need and use case.
      </li>
    </ul>
</ul>  
  <li><b>Drivers</b>: Data, code, artifacts, middleware, and infrastructure - mid and lower layers.</li>
  </p>

<h2>References</h2>
<ul>
  <li><b>[1] </b><a href="https://services.google.com/fh/files/misc/practitioners_guide_to_mlops_whitepaper.pdf">Google MLOps Whitepapers. </a><i>2021</i>.</li>
  <li><b>[2] </b><a href="https://www.amazon.com/Engineering-MLOps-Rapidly-production-ready-learning/dp/1800562888">Book: Engineering MLOPs. Rapidly build, test, and manage production-ready machine learning life cycles at scale. Written by Emmanuel Raj.</a> <i>2021</i>.</li>
</ul>

---

<h2>Python Project Structure for MLOps</h2>

<h3>Main commands to set-up project structure</h3>
<p>The whole project structure must be executed in isolated Virtual Environment which can be created in terminal by typing this command:
  
````
python -m venv env_name
````
  
Once you have created you virtual environment, you can activate it with this command:
  
````
source ˜/.env_name/bin/activate
````
  
 Once you have activated your virtual environment, you can check it where the activated Python kernel is located by typing <code>which python</code> in your terminal. The appeared located must match with location of your virtual environment rood directory. The next step is to locate to the directory where <i>requirements.txt</i> is located and install all required dependencies for the project with this command:
  
````
pip install -r requirements.txt
````
  
</p>

<h3>Organizing Project Structure</h3>
<p>
  For MLOps purposes the suggesting Data Science project structure should consists of following files:
  <ul>
    <li><i>Makefile</i>.</li>
    <li><i>requirements.txt</i>.</li>
    <li><i>hello.py</i> - for demonstrating purposes.</li>
    <li><i>test_hello.py</i> - for demonstrating purposes.</li>
    <li><i>virtualenv</i> - (Virtual environment).</li>
  </ul><br>
  This structure must be dominated in any Github repository to be able it deploy, or transfer to any cloud system.</p>
  
  <p>
  Suggesting example of <i>Makefile</i> is represented below.
  
````
install
    pip install --upgrade pip &&\
        pip install -r requirements.txt

format
    black *.py

lint:
    pylint --disable=R,C hello.py

test:
    python -m pytest -vv --cov=hello test_hello.py
````

  To construct <i>Makefile</i> always use Tabs, not Spaces. You can use the same <i>Makefile</i> over and over again for the projects.<br>
  If you want to launch specifically <i>lint</i> part, type <code>make lint</code> in your terminal.
</p>
