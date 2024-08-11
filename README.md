# Adobe-GenSolve

<h1>CURVETOPIA</h1>

<h2>Introduction:</h2>
<p>Welcome to CURVETOPIA: A Journey into the World of Curves. This project explores the fascinating realm of 2D curves, focusing on their identification, regularization, and beautification in Euclidean space. Our work addresses three primary challenges in computational geometry and computer vision: curve regularization, symmetry detection, and curve completion.</p>



<h2>Objective:</h2>
<p>Our mission is to develop a robust system that can process 2D curves, transforming raw input into well-defined, aesthetically pleasing geometric forms. We aim to create an end-to-end process that takes line art as input and outputs a set of curves defined as connected sequences of cubic Bezier curves.</p>

<h2>Problem Statement:</h2>
<p>While our ultimate goal is to work with PNG (raster) images of line art, we've started with a simplified approach. Our current input consists of polylines, defined as sequences of points in R². Specifically, we work with a finite subset of paths from P, where P is the set of all paths in R². Each path is a finite sequence of points {pi}1≤i≤n from R².</p>

<p>Our task is to transform this input into another set of paths that exhibit the desired properties of regularization, symmetry, and completeness. For visualization purposes, we use the SVG format, which can be rendered in a browser, with the output curves represented as cubic Bézier curves.</p>

<h2>Key Challenges:</h2>
<ol>
  <li><strong>Curve Regularization:</strong> We identify and regularize various shapes within the given set of curves. This includes detecting and refining primitives such as straight lines, circles, ellipses, rectangles (including rounded rectangles), regular polygons, and star shapes.</li>
  <li><strong>Symmetry Exploration:</strong> For closed shapes, we detect the presence of symmetry, focusing primarily on reflection symmetries. This involves identifying lines of symmetry where the shape can be divided into mirrored halves.</li>
  <li><strong>Curve Completion:</strong> We address the challenge of completing curves that have been "planarized" due to overlapping portions being removed. This task requires us to naturally complete curves with gaps or partial holes.</li>
</ol>

<h2>Methodology:</h2>
<p>Our approach to analysing and processing the fragment images consists of four main steps: shape regularization, line smoothening, symmetry detection, and occlusion handling. Each step is designed to enhance and extract specific features from the input images.</p>

<h3>1. Shape Regularization:</h3>
<p>In this step, we focus on identifying and regularizing various shapes within the fragment image. The process involves the following key steps:</p>
<ol>
  <li>Image Preprocessing:
    <ul>
      <li>Convert the input image to grayscale.</li>
      <li>Apply binary thresholding to create a black and white image.</li>
    </ul>
  </li>
  <li>Contour Detection:
    <ul>
      <li>Use OpenCV's findContours function to identify shapes in the binary image.</li>
    </ul>
  </li>
  <li>Shape Classification:
    <ul>
      <li>For each contour, calculate circularity and detect corners.</li>
      <li>Classify shapes based on these properties into categories such as circles, rectangles, triangles, pentagons, and stars.</li>
    </ul>
  </li>
  <li>Shape Regularization:
    <ul>
      <li>Draw regularized versions of the detected shapes on a new image.</li>
      <li>Use specific drawing methods for each shape type (e.g., cv2.circle for circles, cv2.rectangle for rectangles).</li>
    </ul>
  </li>
  <li>Special Handling for Stars:
    <ul>
      <li>Implement a custom algorithm to detect and draw star shapes accurately.</li>
    </ul>
  </li>
</ol>

<h3>2. Line Regularization:</h3>
<p>After shape regularization, we focus on enhancing the linear features in the image. The line smoothening process includes:</p>
<ol>
  <li>Edge Detection:
    <ul>
      <li>Apply Canny edge detection to identify edges in the image.</li>
    </ul>
  </li>
  <li>Hough Line Transform:
    <ul>
      <li>Use the probabilistic Hough Line Transform (cv2.HoughLinesP) to detect line segments in the edge image.</li>
    </ul>
  </li>
  <li>Line Drawing:
    <ul>
      <li>Create a blank white canvas.</li>
      <li>Draw the detected lines on this canvas, resulting in a cleaner representation of the linear features.</li>
    </ul>
  </li>
</ol>

<h3>3. Symmetry Detection:</h3>
<p>Symmetry detection is performed to identify any symmetric properties in the fragment, which can be valuable for reconstruction purposes. The symmetry detection algorithm involves:</p>
<a href="http://www.cse.psu.edu/~yul11/CourseFall2006_files/loy_eccv2006.pdf">The reffered research paper</a>
<ol>
  <li>Feature Extraction:
    <ul>
      <li>Use SIFT (Scale-Invariant Feature Transform) to detect key points and compute descriptors.</li>
    </ul>
  </li>
  <li>Feature Matching:
    <ul>
      <li>Match SIFT features between the original image and its mirrored version.</li>
    </ul>
  </li>
  <li>Symmetry Analysis:
    <ul>
      <li>Calculate potential lines of symmetry using a Hough-like approach.</li>
      <li>Compute symmetry scores based on matched features and their orientations.</li>
    </ul>
  </li>
  <li>Symmetry Determination:
    <ul>
      <li>Decide if the image is symmetric based on the number and quality of feature matches.</li>
      <li>If symmetric, identify the dominant line of symmetry.</li>
    </ul>
  </li>
</ol>

<h3>4. Occlusion:</h3>
<p>The code performs shape detection and completion on input fragments. This process involves:</p>
<ol>
  <li>CSV Parsing:
    <ul>
      <li>Read input CSV file containing polyline data.</li>
      <li>Group points by path and sub path.</li>
    </ul>
  </li>
  <li>Shape Detection:
    <ul>
      <li>For each polyline, detect the shape based on circularity and number of corners.</li>
      <li>Shapes are categorized as circles, rectangles, triangles, pentagons, stars, or unknown.</li>
    </ul>
  </li>
  <li>Shape Completion:
    <ul>
      <li>If a shape is detected as occluded (fewer points than expected), complete it.</li>
      <li>Different completion methods for different shapes (e.g., circle, star).</li>
    </ul>
  </li>
</ol>

<h2>Conclusion:</h2>
<p>CURVETOPIA presents a comprehensive approach to analysing and processing 2D curves, addressing key challenges in computational geometry and computer vision. Through a multi-step process involving shape regularization, line smoothening, symmetry detection, and occlusion handling, the project demonstrates significant progress in transforming raw input into well-defined, aesthetically pleasing geometric forms.</p>

<p>The implemented algorithms show promise in accurately detecting and regularizing various shapes, enhancing linear features, identifying symmetries, and completing occluded shapes. This end-to-end process provides a solid foundation for working with line art and transforming it into connected sequences of cubic Bezier curves.</p>

<p>While the current implementation focuses on polyline input, the methodologies developed have the potential to be extended to more complex raster image inputs in the future. The project's modular approach allows for further refinement and expansion of each component, paving the way for more sophisticated curve processing techniques.</p>
