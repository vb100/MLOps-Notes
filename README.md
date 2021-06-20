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
  
all: install lint test
````

  To construct <i>Makefile</i> always use Tabs, not Spaces. You can use the same <i>Makefile</i> over and over again for the projects.<br>
  If you want to launch specifically <i>lint</i> part, type <code>make lint</code> in your terminal. Alternatively, to launch <i>format</i> part, type <code>make format</code> in your terminal.<br>
  By running <code>make all</code> you can run the whole pipeline in one line.<br>
  Recommended <i>requirements.txt</i> contect is this.

````
pylint
pytest
click
black
pytest-cov
````
  
We do not specify versions of these packages assuming the we will use the newest ones. This list of modules can be extended by adding those ones which are rquired for your case or project.
  
  The example of <i>test_hello.py</i> can be the following code:
  
````
from hello import add
  
def test_add()
    assert add(1, 2) == 3
````
</p>

You can define as many test files as you want for usual and extreme use cases.

<h3>Github Actions</h3>
<p>
  In case you want to set-up your github action for your project, click on <i>setup a workflow yourself</i> and you will be re-directed to <i>you_project/.github/workflows/<b>main.yml</b></i>.<br>
  In this file you are telling the system when you push something to the <i>master</i>/<i>main</i> branch, and can be something like this represented below.
  
````
name: Python application test with Github action
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python 3.8
        uses: actions/setup-python@v1
        with:
          python-version: 3.8
      - name: Install dependencies
        run: |
          make install
      - name: Lint with Python
        run: |
          make lint
      - name: Test with Python
        run: |
          make test
      - name: Format code with Python black
        run: |
          make: format
````
  
You can have as many of these files as you want. For every single file that runs, it will exactly do what you say. For example, if we want to later setup a Google based deployment, we can set that up. If we want to set up an Azure based testing project, we can go ahead and set that up. <br>
  You can check the performance of your Github actions by clicking on <b>Actions</b> in the top menu on you Github. On the top of that, you can create a special link to your <i>Readme.md</i> file which will dynamically shows-up the status of your selected Github action. For this, choose and click on <i>Create status badge</i> in your Github action window. This is an useful aspect of a SaaS based continuous integration (<i>CI</i>) system.
</p>

<h3>Testing</h3>
<p>
There are following tpyes of tests:
  <ul>
    <li>Unit</li>
    <li>Integration</li>
    <li>Functional</li>
    <li>End-to-End</li>
    <li>Acceptance</li>
    <li>Performance</li>
    <li>Exploratory</li>
    </ul>
</p>

<h3>Get SSH Key</h3>
<p>
  You can create your new SSH key for your new virtual environment by type <code>ssh-keygen -t rsa</code> in your terminal activated within your virtual environment. From here, you can print-out how public key is looks like by typing <code>cat /home/<your_name>/.ssh/id_rsa</code>.<br>
  Then go yo your Github account. There go to <i>Settings</i>, then go to <i>SSH and GPG keys</i>, type the new name of the key and paste the public key into <i>Key</i> section (starting with <i>ssh-rsa</i>).
</p>

  <h2>Continuous Delivery and Continuous Integration</h2>
  <h3>What is Continuous Delivery</h3>
  <p>Continuous Delivery (furthermore <i>CD</i>) is a term which means that the code is always in a deployable state, both in term of application software and the infrastructure needed to run the code.</p>
  <p><b>Example.</b> You as the user, you may be developing code on your laptop, and you are checking your code into a source control repository. And you would have the <i>master branch</i> which is the default branch in GitHub be the place where it would be hooked up to a particular environment. When you make the change a build server, and this could be many different types:
<ul>
  <li>Github</li>
  <li>Jenkins</li>
  <li>AWS Code Built</li>
  </ul>
  Here you can <i>lint</i>, <i>deploy</i>, and <i>test</i> your code. And then it looks at the infrastructure as code (<b>IaC</b>) and this could be :
  <ul>
  <li>Terraform</li>
  <li>Cloud Formation</li>
  <li>Other kind of infrastructure...</li>
  </ul></p><p>
  This <b>IaC</b> allows you to dynamically update a new environment or even create one. And that environment will be directly mapped to the branch in your source control. <br>
For example, you could have a <i>development</i> branch. You could have a <i>staging</i> branch, and you could have a <i>production</i> branch. And each one of those situations, those branches could automatically create a parallel environment.<br>
You could push your code into a <i>development</i> branch. And then when you are ready to test a change, that would be something that would go to <i>production</i> later, you can merge it into the <i>staging</i> branch. It will automatically go through <i>lint</i> code, <i>test</i> your code, <i>deploy</i> it to your <i>staging environment</i>, you could then do a very extensive <b>load test</b> to verify that your web application could scale to 100,000 users.<br>
And then after that is done, you say, great, let's go ahead and merge it to <i>production</i> and it could go directly into production. 
  </p>
