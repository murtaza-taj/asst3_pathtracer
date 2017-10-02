# Assignment 2-1: Ray Tracing Part 1


<!doctype html>
<html>
<head>
<link rel="icon" href="https://cs184.org/assets/images/favicon/cal_200.png" type="image/png">
<title>Project 3-1: Ray Tracing Part 1 : CS184 : Spring 2017</title>

<!--[if lt IE 9]>
<script>
    if (confirm("This site is *known buggy* on versions of Internet Explorer less than IE9. Do you want to download a modern browser instead?")) {
        window.location = "https://www.google.com/intl/en/chrome/browser/";
    }
</script>
<![endif]-->

<script>
  (function(d, s, id){
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) {return;}
    js = d.createElement(s); js.id = id;
    js.src = "https://assets.gfycat.com/gfycat.js";
    fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'gfycat-js'));
</script>

<script src="https://use.edgefonts.net/open-sans:n3,i3,n4,i4,n6,i6,n7,i7,n8,i8.js"></script>
<script src="https://use.edgefonts.net/open-sans-condensed:n3,i3,n7.js"></script>

<script src="https://cs184.org/assets/third_party/jquery/1.8.3/jquery.min.js"></script>
<script src="https://cs184.org/assets/third_party/jquery/timeago/jquery.timeago.js"></script>
<script src="https://cs184.org/assets/third_party/jquery/cookie/jquery.cookie.js"></script>

<script src="https://cs184.org/assets/third_party/codemirror-3.0/lib/codemirror.js"></script>
<script src="https://cs184.org/assets/third_party/codemirror-3.0/mode/markdown/markdown.js"></script>
<link rel="stylesheet" type="text/css" href=" https://cs184.org/assets/third_party/codemirror-3.0/lib/codemirror.css">

<script src="https://cs184.org/assets/third_party/google-code-prettify/prettify.js"></script>
<link rel="stylesheet" type="text/css" href=" https://cs184.org/assets/third_party/google-code-prettify/prettify.css">

<!-- NOTE(kayvonf): place at end to override 3rd party tools -->
<link rel="stylesheet" type="text/css" href=" https://cs184.org/assets/css/main.css">

<script type="text/javascript">
var edit_comment_url = "https://cs184.org/comments/ajax_edit_comment";
var delete_comment_url = "https://cs184.org/comments/ajax_delete_comment";
var archive_comment_url = "https://cs184.org/comments/ajax_archive_comment";
var add_private_comment_url = "https://cs184.org/comments/ajax_add_private_comment";
var add_instructor_comment_url = "https://cs184.org/comments/ajax_add_instructor_comment";
var add_comment_url = "https://cs184.org/comments/ajax_add_comment";
var comment_vote_url = "https://cs184.org/comments/ajax_comment_vote";
var toggle_subscribe_url = "https://cs184.org/comments/ajax_toggle_subscribe";
var prompt_students_url = "https://cs184.org/comments/ajax_prompt_students";
var keep_alive_url = "https://cs184.org/keep_alive";
</script>

<script type="text/javascript" src="https://cs184.org/assets/js/main.js"></script>
<script type="text/javascript" src="https://cs184.org/assets/js/comments.js"></script>

</head>
<body>

<div id="modal_overlay"></div>

<div class="main_container">

<div class="topbarbackground">
<div class="topbar">
<div class="topbar_left"><a href="https://cs184.org/">Home</a></div>
<div class="topbar_left"><a href="https://cs184.org/courseinfo">Info</a></div>
<div class="topbar_left"><a href="https://cs184.org/article/2">Readings</a></div>
<div class="topbar_left"><a href="https://cs184.org/article/8">Sections</a></div>
<div class="topbar_left"><a href="https://cs184.org/newsfeed">Feed</a></div>
<!--
<div class="topbar_left"><a href="https://cs184.org/exercises">[Exercises]</a></div>
<div class="topbar_left"><a href="https://cs184.org/competition">[Competition]</a></div>
-->



<div class="topbar_right">

<a href="https://cs184.org/users/login">Login</a>

</div>

</div>
</div>

<div class="content_container">

<!-- renng: commenting this out; not sure why it's here'
</body>
-->

<!-- end of header -->





<div class="article_container">

<div class="common_title title">Project 3-1: Ray Tracing Part 1</div>

<hr size="1">


<div class="markdown article-content">
<p><center>
<img src="/uploads/article_images/12_.jpg" width="800px" />
</center></p>

<h2>Due Date</h2>

<p>Wed Oct 11th, 11:59pm</p>

<h2>Overview</h2>

<p>You will implement the core routines of a physically-based renderer using a pathtracing algorithm. This assignment reinforces many of the hefty ideas covered in class recently, including ray-scene intersection, acceleration structures, and physically based lighting and materials. By the time you are done, you'll be able to generate some stunning pictures (given enough patience and CPU time). You will also have the chance to extend the assignment in a plethora of technically challenging and intellectually stimulating directions.</p>

<h2>Project Parts</h2>

<p>This time, we've split off each part into its own article:</p>

<ul>
<li>Part 1: <a href="/article/13">Ray Generation and Scene Intersection</a></li>
<li>Part 2: <a href="/article/14">Bounding Volume Hierarchy</a></li>
<li>Part 3: <a href="/article/15">Direct Illumination</a></li>
<li>Part 4: <a href="/article/16">Indirect Illumination</a></li>
<li>Part 5: <a href="/article/17">Adaptive Sampling</a></li>
</ul>

<p>All parts are equally weighted at 20 points each, for a total of 100 points.</p>

<p>You'll also want to read these articles:</p>

<ul>
<li><a href="/article/18">Website Writeup and Deliverables</a></li>
<li><a href="/article/19">Extra Credit Opportunities</a></li>
</ul>

<h2>Using the program</h2>

<p><a href="https://gitlab.com/cs184/proj3_1_pathtracer/repository/archive.zip?ref=master">Download</a> the zipped assignment or clone it from <a href="https://gitlab.com/cs184/proj3_1_pathtracer">Gitlab</a>:</p>

<pre><code>git clone https://gitlab.com/cs184/proj3_1_pathtracer.git
</code></pre>

<p>As before, use <em>cmake</em> and <em>make</em> inside a <em>build/</em> directory to create the executable (<a href="/article/7">how to build and submit</a>).</p>

<h3>Command line options</h3>

<p>Use these flags between the executable name and the <em>dae</em> file when you invoke the program. For example, to simply run the regular GUI with the <em>CBspheres.dae</em> file and 8 threads, you could type:</p>

<pre><code>./pathtracer -t 8 ../dae/sky/CBspheres_lambertian.dae
</code></pre>

<p>If you wanted to save to the <em>spheres_64_16_6.png</em> file on the instructional machines with 64 samples per pixel, 16 samples per light, 6 bounce ray depth, and 480x360 resolution, you might rather use something like this:</p>

<pre><code>./pathtracer -t 8 -s 16 -l 4 -m 6 -r 480 360 -f spheres_16_4_6.png ../dae/sky/CBspheres_lambertian.dae
</code></pre>

<p>For this assignment, we've provided a windowless run mode, which is triggered by providing a filename with the <code>-f</code> flag. The program will run in this mode when you are <em>ssh</em>-ed into the instructional machines.</p>

<p>This means that when trying to generate high quality results for your final writeup, you can use the windowless mode to farm out long render jobs to the s349 machines! You'll probably want to use <a href="https://www.howtoforge.com/linux_screen"><em>screen</em></a> to keep your jobs running after you logout of <em>ssh</em>. After the jobs complete, you can view them using the <em>display</em> command, assuming you've <em>ssh</em>-ed in with graphics forwarding enabled (by using the <code>-Y</code> flag).</p>

<p>Also, please take note of the <code>-t</code> flag! We recommend running with 4-8 threads almost always -- the exception is that you should use <code>-t 1</code> when debugging with print statements, since <code>printf</code> and <code>cout</code> are not thread safe.</p>

<table>
<thead>
<tr>
  <th>Flag and parameters</th>
  <th align="center">Description</th>
</tr>
</thead>
<tbody>
<tr>
  <td><code>-s  &lt;INT&gt;</code></td>
  <td align="center">Number of camera rays per pixel (default=1, should be a power of 2)</td>
</tr>
<tr>
  <td><code>-l  &lt;INT&gt;</code></td>
  <td align="center">Number of samples per area light (default=1)</td>
</tr>
<tr>
  <td><code>-t  &lt;INT&gt;</code></td>
  <td align="center">Number of render threads (default=1)</td>
</tr>
<tr>
  <td><code>-m  &lt;INT&gt;</code></td>
  <td align="center">Maximum ray depth (default=1)</td>
</tr>
<tr>
  <td><code>-f  &lt;FILENAME&gt;</code></td>
  <td align="center">Image (.png) file to save output to in windowless mode</td>
</tr>
<tr>
  <td><code>-r  &lt;INT&gt; &lt;INT&gt;</code></td>
  <td align="center">Width and height in pixels of output image (if windowless) or of GUI window</td>
</tr>
<tr>
  <td><code>-c  &lt;FILENAME&gt;</code></td>
  <td align="center">Load camera settings file &#40;mainly to set camera position when windowless&#41;</td>
</tr>
<tr>
  <td><code>-h</code></td>
  <td align="center">Print command line help message</td>
</tr>
</tbody>
</table>

<h3>Moving the camera (in edit and BVH mode)</h3>

<table>
<thead>
<tr>
  <th>Command</th>
  <th align="center">Action</th>
</tr>
</thead>
<tbody>
<tr>
  <td>Rotate</td>
  <td align="center">Left-click and drag</td>
</tr>
<tr>
  <td>Translate</td>
  <td align="center">Right-click and drag</td>
</tr>
<tr>
  <td>Zoom in and out</td>
  <td align="center">Scroll</td>
</tr>
<tr>
  <td>Reset view</td>
  <td align="center">Spacebar</td>
</tr>
</tbody>
</table>

<h3>Keyboard commands</h3>

<table>
<thead>
<tr>
  <th>Command</th>
  <th align="center">Keys</th>
</tr>
</thead>
<tbody>
<tr>
  <td>Mesh-edit mode (default)</td>
  <td align="center"><code>E</code></td>
</tr>
<tr>
  <td></td>
  <td align="center"></td>
</tr>
<tr>
  <td>BVH visualizer mode</td>
  <td align="center"><code>V</code></td>
</tr>
<tr>
  <td>Descend to left/right child (BVH viz)</td>
  <td align="center"><code>LEFT/RIGHT</code></td>
</tr>
<tr>
  <td>Move up to parent node (BVH viz)</td>
  <td align="center"><code>UP</code></td>
</tr>
<tr>
  <td></td>
  <td align="center"></td>
</tr>
<tr>
  <td>Start rendering</td>
  <td align="center"><code>R</code></td>
</tr>
<tr>
  <td>Save a screenshot</td>
  <td align="center"><code>S</code></td>
</tr>
<tr>
  <td>Decrease/increase area light samples</td>
  <td align="center"><code>- +</code></td>
</tr>
<tr>
  <td>Decrease/increase camera rays per pixel</td>
  <td align="center"><code>[ ]</code></td>
</tr>
<tr>
  <td>Decrease/increase maximum ray depth</td>
  <td align="center"><code>&lt; &gt;</code></td>
</tr>
<tr>
  <td>Toggle cell render mode</td>
  <td align="center"><code>C</code></td>
</tr>
<tr>
  <td>Dump camera settings to file &#40;including position&#41;</td>
  <td align="center"><code>D</code></td>
</tr>
</tbody>
</table>

<p>Cell render mode lets you use your mouse to highlight a region of interest so that you can see quick results in that area when fiddling with per pixel ray count, per light ray count, or ray depth.</p>

<h2>Basic code pipeline</h2>

<p>What happens when you invoke <em>pathtracer</em> in the starter code? Logistical details of setup and parallelization:</p>

<ol>
<li>The <code>main()</code> function inside <em>main.cpp</em> parses the scene file using a <code>ColladaParser</code> from <em>collada/collada.h</em>.</li>
<li>A new <code>Viewer</code> and <code>Application</code> are created. <code>Viewer</code> manages the low-level OpenGL details of opening the window, and it passes most user input into <code>Application</code>. <code>Application</code> owns and sets up its own <code>pathtracer</code> with a camera and scene. </li>
<li>An infinite loop is started with <code>viewer.start()</code>. The GUI waits for various inputs, the most important of which launch calls to <code>set_up_pathtracer()</code> and <code>PathTracer::start_raytracing()</code>. </li>
<li><code>set_up_pathtracer()</code> sets up the camera and the scene, notably resulting in a call to <code>PathTracer::build_accel()</code> to set up the BVH.</li>
<li>Inside <code>start_raytracing()</code> (implemented in <em>pathtracer.cpp</em>), some machinery runs to divide up the scene into "tiles," which are put into a work queue that is processed by <code>numWorkerThreads</code> threads.</li>
<li>Until the queue is empty, each thread pulls tiles off the queue and runs <code>raytrace_tile()</code> to render them. <code>raytrace_tile()</code> calls <code>raytrace_pixel()</code> for each pixel inside its extent. The results are dumped into the pathtracer's <code>sampleBuffer</code>, an instance of an <code>HDRImageBuffer</code> (defined in <em>image.h</em>).</li>
</ol>

<p>Most of the core rendering loop is left for you to implement.</p>

<ol>
<li>Inside <code>raytrace_pixel()</code>, you will write a loop that calls <code>camera-&gt;generate_ray(...)</code> to get camera rays and <code>trace_ray(...)</code> to get the radiance along those rays.</li>
<li>Inside <code>trace_ray</code>, you will check for a scene intersection using <code>bvh-&gt;intersect(...)</code>. If there is an intersection, you will accumulate the return value in <code>Spectrum L_out</code>, 

<ul>
<li>adding the BSDF's emission with <code>bsdf-&gt;get_emission()</code> if appropriate, </li>
<li>adding direct lighting with <code>estimate_direct_lighting(...)</code>, and </li>
<li>adding indirect lighting with <code>estimate_indirect_lighting(...)</code>, which will recurse to call <code>trace_ray</code> once more.</li>
</ul></li>
</ol>

<p>You will also be implementing the functions to intersect with triangles, spheres, and bounding boxes, the functions to construct and traverse the BVH, and the functions to sample from various BSDFs.</p>

<p>Approximately in order, you will edit (at least) the files</p>

<ul>
<li><em>pathtracer.cpp</em> (part 1)</li>
<li><em>camera.cpp</em> (part 1)</li>
<li><em>static_scene/triangle.cpp</em> (part 1)</li>
<li><em>static_scene/sphere.cpp</em> (part 1)</li>
<li><em>bvh.cpp</em> (part 2)</li>
<li><em>bbox.cpp</em> (part 2)</li>
<li><em>bsdf.cpp</em> (part 3)</li>
<li><em>pathtracer.cpp</em> (parts 3-5)</li>
</ul>

<p>You will want to skim over the files</p>

<ul>
<li><em>ray.h</em></li>
<li><em>intersection.h</em></li>
<li><em>sampler.h/cpp</em></li>
<li><em>random_util.h</em></li>
<li><em>static_scene/light.h/cpp</em></li>
</ul>

<p>since you will be using the classes and functions defined therein.</p>

<h2>Rendering Competition Part 1</h2>

<p>If you participate in this assignment's rendering competition, we will require you to submit both a <em>competition.png</em> image and a short 5-10 sentence description of what you did to create your entry. You can choose to either emphasize the technical or artistic/modeling merits of your image. If you go the artistic route, you should generate the model yourself using Blender or procedural code that you write. If you go the technical route, you may use models downloaded from the internet, but you should emphasize the extra algorithms you implemented in your short writeup.</p>

<p>Possible ideas include but not limited to: making complicated scenes, making cool shadows (by customizing your light sources and manipulating objects), making short videos (by writing a script that generates a .dae file per frame), etc. Just be creative!</p></div>




</div>

</div>  <!-- end of content_container (defined in header.php) -->
</div>  <!-- end main_container (defined in header.php) -->

<hr size="1">
<div class="footer" >
<div class="footer_right" style="padding-bottom: 1em;">
Copyright 2017 UC Berkeley
</div>
</div>


<script type="text/javascript" src="//cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$']],
        displayMath: [['$$', '$$'], ['\\[', '\\]']],
        processEscapes: true
    },
    messageStyle: "none",
    "HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX", "TeX"] }
});
</script>

</body>
</html>

