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

<h2>References</h2>
<ul>
  <li><b>[1] </b><a href="https://services.google.com/fh/files/misc/practitioners_guide_to_mlops_whitepaper.pdf">Google MLOps Whitepapers. <i>2021</i>.</a></li>
  <li><b>[1] </b><a href="https://www.amazon.com/Engineering-MLOps-Rapidly-production-ready-learning/dp/1800562888">Book: Engineering MLOPs. Rapidly build, test, and manage production-ready machine learning life cycles at scale. Written by Emmanuel Raj. <i>2021</i>.</a></li>
</ul>
