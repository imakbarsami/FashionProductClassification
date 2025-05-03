
<body>

  <header>
    <h1>👗 Fashion Product Classification</h1>
    <p>
      A deep learning–based system for automated categorization of fashion items,  
      developed as part of the Neural Network and Fuzzy Logic course (CSE 451, Fall 2024)  
      at Premier University, Chittagong.
    </p>
    <nav>
      <ul>
        <li>Overview</li>
        <li>Repo Structure</li>
        <li>Dataset</li>
        <li>Methodology</li>
        <li>Results</li>
        <li>Model Testing</li>
        <li>Error Analysis</li>
        <li>Team &amp; Contact</li>
      </ul>
    </nav>
  </header>

  <section id="overview">
    <h2>📖 Project Overview</h2>
    <p>
      In this project, we explore transfer learning with six state-of-the-art CNN architectures  
      (EfficientNetV2M, NASNetLarge, ResNet50, Xception, InceptionV3, DenseNet201)  
      to classify real-world fashion product images into 54 primary categories (e.g., Tshirts, Jeans, Sandals).
      We leverage TPU v3-8 acceleration, extensive preprocessing, and fine-tuning to achieve robust performance.
    </p>
  </section>

  <section id="structure">
    <h2>📂 Repository Structure</h2>
    <table>
      <tr><th>File</th><th>Description</th></tr>
      <tr>
        <td><code>fashion-product-classification.ipynb</code></td>
        <td>Project implementation &amp; code walkthrough (EDA, preprocessing, model definitions, training).</td>
      </tr>
      <tr>
        <td><code>ModelTesting.ipynb</code></td>
        <td>Model rebuild &amp; inference scripts; real-world image predictions.</td>
      </tr>
      <tr>
        <td><code>FashionProductClassification.pdf</code></td>
        <td>Final report: abstract, literature review, methodology, results, error analysis, conclusions.</td>
      </tr>
      <tr>
    </table>
  </section>

  <section id="dataset">
    <h2>📦 Dataset</h2>
    <ul>
      <li>Source: Kaggle “Fashion Product Images Dataset” (44,424 entries).</li>
      <li>Filtered to 42,150 images across 54 article types (95% of distribution).</li>
      <li>Train/Val/Test split: 80% / 10% / 10% (33,720 / 4,215 / 4,215 images).</li>
      <li>Features: gender, masterCategory, subCategory, articleType, baseColour, season, year, usage.</li>
    </ul>
  </section>

  <section id="methodology">
    <h2>🛠️ Methodology</h2>
    <ol>
      <li><strong>Exploratory Data Analysis</strong>  
        – Distribution of classes, handling missing values, imbalance analysis.</li>
      <li><strong>Preprocessing</strong>  
        – Resize with padding; model-specific normalization; optional augmentation (flip, rotation).</li>
      <li><strong>Model Building</strong>  
        – Load each ImageNet-pretrained base; unfreeze last N layers; append GAP, Dense(2048→softmax).</li>
      <li><strong>Training</strong>  
        – TPU v3-8 distributed training; Adam optimizer with LR decay; early stopping; model checkpointing.</li>
      <li><strong>Evaluation</strong>  
        – Metrics: validation accuracy, test accuracy, macro-AUPRC; confusion matrices; class-wise F1.</li>
    </ol>
    <h3>Model Configurations</h3>
    <table>
      <tr><th>Model</th><th>Input Size</th><th>Trainable Layers</th></tr>
      <tr><td>NASNetLarge</td><td>331×331</td><td>Last 20</td></tr>
      <tr><td>EfficientNetV2M</td><td>299×299</td><td>Last 10</td></tr>
      <tr><td>Xception</td><td>299×299</td><td>Last 15</td></tr>
      <tr><td>InceptionV3</td><td>299×299</td><td>Last 15</td></tr>
      <tr><td>ResNet50</td><td>224×224</td><td>Last 10</td></tr>
      <tr><td>DenseNet201</td><td>224×224</td><td>Last 20</td></tr>
    </table>
  </section>

  <section id="results">
    <h2>📊 Key Results</h2>
    <table>
      <tr><th>Model</th><th>Test Accuracy</th><th>Macro-AUPRC</th></tr>
      <tr><td>NASNetLarge</td><td>93.19%</td><td>0.9475</td></tr>
      <tr><td>EfficientNetV2M</td><td>93.07%</td><td>0.9389</td></tr>
      <tr><td>Xception</td><td>92.91%</td><td>0.9437</td></tr>
      <tr><td>DenseNet201</td><td>92.55%</td><td>0.9410</td></tr>
      <tr><td>InceptionV3</td><td>92.29%</td><td>0.9441</td></tr>
      <tr><td>ResNet50</td><td>92.15%</td><td>0.9341</td></tr>
    </table>
    <p>
      <em>NASNetLarge</em> emerged as the top performer, followed closely by EfficientNetV2M and Xception.
    </p>
  </section>

  <section id="testing">
    <h2>🧪 Model Testing</h2>
    <p>ResNet50V2 was exported for inference on unseen images.  
       We tested on both color and black-and-white product images:</p>
    <ul>
      <li>Color images: T-shirts, Jeans, Sandals, Earrings, Socks – all correctly classified.</li>
      <li>Black-and-white images: Sandals, Earrings – robust to grayscale input.</li>
    </ul>
    <p>See <code>ModelTesting.ipynb</code> for code snippets and sample outputs.</p>
  </section>

  <section id="error-analysis">
    <h2>🔍 Error Analysis</h2>
    <p>Certain visually similar pairs remain challenging:</p>
    <table>
      <tr><th>True</th><th>Predicted</th><th>Count</th></tr>
      <tr><td>Tshirts</td><td>Tops</td><td>26</td></tr>
      <tr><td>Sports Shoes</td><td>Casual Shoes</td><td>19</td></tr>
      <tr><td>Flats</td><td>Heels</td><td>17</td></tr>
      <tr><td>Casual Shoes</td><td>Sports Shoes</td><td>17</td></tr>
      <tr><td>Formal Shoes</td><td>Flats</td><td>16</td></tr>
    </table>
    <p>Root causes include feature overlap, lighting/background variations, and class imbalance.</p>
  </section>

  <section id="authors">
    <h2>👥 Team &amp; Contact</h2>
    <ul>
      <li><strong>Md Ali Akbar Sami</strong>  
        <br>Email: mdsamipuc@gmail.com</li>
      <li><strong>Sakib Chowdhury</strong>  
        <br>Email: sakibchy.bban.puc@gmail.com</li>
      <li><strong>Puspita Bhattacharjee</strong>  
        <br>Email: puspitapuc@gmail.com</li>
    </ul>
    <p>
      Dept. of CSE, Premier University, Chittagong  
      <br>For questions or collaboration, feel free to reach out.
    </p>
  </section>

  <footer>
    &copy; 2025 Fashion Product Classification Team. All rights reserved.
  </footer>

</body>
</html>
