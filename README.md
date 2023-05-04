Download Link: https://assignmentchef.com/product/solved-csc225-algorithms-and-data-structures-i-programming-assignment-3
<br>
<strong>Note</strong>: Demos will be held during the week of July 31st, 2017 (which is the first week of the exam period). If you are unable to attend any of the demos during that week (for example, because of travel plans), you may schedule a demo during the last week of classes. This will require you to hand the assignment in early. Please contact your instructor <strong>immediately </strong>if you need such an arrangement. If you wait until the last minute to make arrangements for an early demo, it may not be possible to accommodate you.

<h1>1              Assignment Overview: Images and Graphs</h1>

This assignment covers an application of graph algorithms to image processing. You will implement a data structure to represent images as graphs, with each pixel of the image represented by a vertex. Then, you will apply various graph traversal algorithms to perform various image manipulations, including the classic ‘flood fill’ operation.

Sections 2 and 3 describe a graph abstraction for colour images which uses edges to connect neighbouring pixels which have the same colour. Section 4 summarizes the tasks to perform for the assignment. Section 5 describes the image viewer interface provided with the assignment code.

<h1>2              Images</h1>

Images can be represented by 2-dimensional arrays of pixels, each with a colour value. Usually, colour values are expressed as a triple (<em>r,g,b</em>) of red, green and blue values. Many image processing tasks work entirely with individual pixel values. For example, to convert an image from colour to greyscale, the colour value of each pixel can be converted to a shade of grey. For a pixel with colour (<em>r,g,b</em>), one possible conversion formula is to produce a new colour (<em>r</em><sup>0</sup><em>,g</em><sup>0</sup><em>,b</em><sup>0</sup>) where

<em> .</em>

Many image processing tasks use information from neighbouring pixels, or from the entire image. CSC 225 will only cover one technique for image processing. The Department of Computer Science offers an entire course (CSC 205) on 2d graphics and image processing, which covers a broader range of techniques.

Consider the small images in Figure 1 below.

(a) Spiral (16 × 16)                                                      (b) Rainbow (50 × 32)

(c) Heart (32 × 28)                                                                 (d) Flag of Canada (64 × 32)

Figure 1: Four small images.

Each image can be viewed as a grid of pixels. Within an image, groups of adjacent pixels with the same colour are often significant. This assignment, and assignment 5, will cover various algorithms to process contiguous regions inside images. Figures 2, 3 and 4 show the individual pixels of three of the images in Figure 1 above.

Figure 2: A close-up view of Figure 1a.

Figure 3: A close-up view of Figure 1b.

Figure 4: A close-up view of Figure 1c.

<h1>3              Pixel Graphs</h1>

Define the <em>pixel graph </em>of an <em>n</em>×<em>m </em>pixel image to be an undirected graph with a vertex <em>v<sub>xy </sub></em>for each pixel (where 0 ≤ <em>x </em>≤ <em>n</em>−1 and 0 ≤ <em>y </em>≤ <em>m</em>−1), and edges between all pairs of neighbouring pixels with the same colour value. Figures 5, 6 and 7 show the pixel graphs for the images in Figures 2, 3 and 4.

Figure 5: The pixel graph for the image in Figure 1a.

Figure 6: The pixel graph for the image in Figure 1b.

Figure 7: The pixel graph for the image in Figure 1c.

Each connected component of the pixel graph corresponds to a contiguous region containing a single colour in the original image. Vertices with degree 4 correspond to pixels in the interior of their region, while vertices with degree less than 4 correspond to pixels on a boundary.

<h1>4              Assignment Structure</h1>

Your task for this assignment is to implement a data structure called PixelGraph to represent a pixel graph and then implement several graph traversal algorithms using the PixelGraph structure.

The PixelGraph data structure is split between the files PixelGraph.java and PixelVertex.java. The traversal algorithms will be implemented in static methods in the A3Algorithms.java file.

The template for this assignment is divided among four files. You are required to use the provided files as the basis for your submission, and may not change any of the classnames or method signatures inside any of the files, or your submission will not be marked. You are free to add additional classes, methods or instance variables as needed, except as indicated below. You are also permitted to include extra files in your submission. Note that if your submission is missing any files and does not compile, the error will be treated the same way as any other compile error (and you will not be given the opportunity to submit the missing files to recover the marks).

<table width="623">

 <tbody>

  <tr>

   <td width="162">A3Algorithms.java</td>

   <td width="462">Contains      five     static                            methods: FloodFillDFS, FloodFillBFS,OutlineRegionDFS, OutlineRegionBFS and CountComponents which perform various tasks on a PixelGraph instance. Read the comments in the template for more details.<strong>Methods to implement</strong>: FloodFillDFS, FloodFillBFS,OutlineRegionDFS, OutlineRegionBFS and CountComponents.</td>

  </tr>

  <tr>

   <td width="162">ImageViewer225.java</td>

   <td width="462">A graphical interface for viewing and transforming images. This is the ‘main program’ which uses the functionality defined in the other files. It is not necessary to read or understand the code in this file to complete the assignment (although you are encouraged to do so). You are free to modify this program for debugging purposes, but all of your modifications will be discarded before marking. During marking, the original, unmodified ImageViewer225.java will be substituted. You will lose marks if your code does not function correctly (or if a compile error occurs) with the unmodified version of ImageViewer225.java.<strong>Methods to implement</strong>: None.</td>

  </tr>

  <tr>

   <td width="162">PixelGraph.java</td>

   <td width="462">The PixelGraph class implements a data structure for storing a pixel graph.<strong>Methods to implement</strong>: Constructor, getPixelVertex, getWidth, getHeight.(Add other methods or properties as needed)</td>

  </tr>

  <tr>

   <td width="162">PixelVertex.java</td>

   <td width="462">The PixelVertex class implements a data structure to store each vertex of a pixel graph.<strong>Methods to implement</strong>: Constructor, getX, getY, getNeighbours, addNeighbour, removeNeighbour, getDegree, isNeighbour. (Add other methods or properties as needed)</td>

  </tr>

 </tbody>

</table>

<h1>5              Image Viewer Interface</h1>

After compiling all of the template files, the graphical interface can be started with the command

$ java ImageViewer225 image_name.png

The Java stack size may need to be modified (as in assignment 2) to accommodate the memory demands of a recursive DFS implementation. In that case, you should use a command like

$ java -Xss64m ImageViewer225 image_name.png

to increase the stack size (in this case, to 64 megabytes).

Figure 8 shows the image viewer window displaying the file rainbow.png (shown in Figure 1b).

Figure 8: The image viewer window after opening the rainbow.png image.

The mouse wheel can be used to control the zoom level of the displayed image (since most of the test images are small, you will likely want to zoom in on them). The “Count Regions” button will construct a PixelGraph object from the displayed image, then use the CountComponents function in A3Algorithms.java to count the number of connected regions in the image and display the result. Clicking on a pixel of the image will run one of the other algorithms in A3Algorithms.java. To select a different colour, use the “Choose Colour” button. The “Sample Colour” button will allow you to set the colour from a pixel in the active image (by left-clicking on the pixel). Figure 9 shows the result of a model solution after clicking at the location shown with the “Flood Fill (DFS)” algorithm selected. Figure 10 shows the result of a model solution after clicking at the location shown with the “Outline Region (DFS)” algorithm selected. Note that the DFS and BFS versions of both applications (Flood Fill and Outline Region) should produce identical final results.

Figure 9: The image viewer window after applying the “Flood Fill (DFS)” algorithm to rainbow.png image using black as the fill colour.

Figure 10: The image viewer window after applying the “Outline Region (DFS)” algorithm to rainbow.png image using black as the outline colour.

<h1>6              Test Images</h1>

A collection of test images (including the images in Figure 1) have been posted to conneX (under the “Data” tab in the sidebar). The image viewer is capable of loading any image in PNG format, so you can also use externally-obtained images for testing.

<h1>7              Using Outside Code</h1>

You are encouraged to use the features of the Java Standard Library (including any of the data structures it provides) in your code. If you use a standard library data structure, make sure you are aware of the running times of the operations you use, since that will be important for determining the running time of your program.

There should be no need to use large volumes of code from other sources (such as outside libraries or the internet) in this assignment. If you believe that your implementation requires an outside library, talk to your instructor.

If you find a small snippet of code on the internet that you want to use (for example, in a StackOverflow thread), put a comment in your code indicating the source (including a complete URL). Remember that using code from an outside source without citation is plagiarism.

You are encouraged to discuss the assignment with your peers, and even to share implementation advice or algorithm ideas. However, you are not permitted to use any code from another CSC 225 student under any circumstances, nor are you permitted to share your code in any way with any other student (or the internet) until after the marking is complete. Sharing your code with others before marking is completed, or using another student’s code for assistance (even if you do not directly copy it) is plagiarism.

<h1>8              Evaluation</h1>

Submit all .java files needed to compile your assignment electronically via conneX. Your code must compile and run correctly in the Linux environment in ECS 242. If your code does not compile as submitted, you will receive a mark of zero.

This assignment is worth 8% of your final grade and will be marked out of 16 during an interactive demo with an instructor. You will be expected to explain the running time of your algorithms to the evaluator, and may also be asked to explain or justify some aspects of your code. Demos must be scheduled in advance (through an electronic system available on conneX). If you do not schedule a demo time, or if you do not attend your scheduled demo, you will receive a mark of zero.

The marks are distributed among the components of the assignment as follows.

<table width="561">

 <tbody>

  <tr>

   <td width="59"><strong>Marks</strong></td>

   <td width="502"><strong>Component</strong></td>

  </tr>

  <tr>

   <td width="59">3</td>

   <td width="502">The PixelGraph data structure is implemented correctly.</td>

  </tr>

  <tr>

   <td width="59">3</td>

   <td width="502">The FloodFillDFS method in A3Algorithms.java is implemented correctly and runs in <em>O</em>(<em>n</em>) time on a graph with <em>n </em>vertices.</td>

  </tr>

  <tr>

   <td width="59">3</td>

   <td width="502">The FloodFillBFS method in A3Algorithms.java is implemented correctly and runs in <em>O</em>(<em>n</em>) time on a graph with <em>n </em>vertices.</td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="502">The OutlineRegionDFS method in A3Algorithms.java is implemented correctly and runs in <em>O</em>(<em>n</em>) time on a graph with <em>n </em>vertices.</td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="502">The OutlineRegionBFS method in A3Algorithms.java is implemented correctly and runs in <em>O</em>(<em>n</em>) time on a graph with <em>n </em>vertices.</td>

  </tr>

  <tr>

   <td width="59">3</td>

   <td width="502">The CountComponents method in A3Algorithms.java is implemented correctly and runs in <em>O</em>(<em>n</em>) time on a graph with <em>n </em>vertices.</td>

  </tr>

 </tbody>

</table>

If your code is not well organized, or if it is poorly documented, the evaluator may ask you explain any aspects that are unclear. If you are unable to do so, up to 2 marks may be deducted. To be clear, you are not required to have spotless, perfectly organized code, but you should be prepared to explain any hard-to-read parts of your code.

You are permitted to delete and resubmit your assignment as many times as you want before the due date, but no submissions or resubmissions will be accepted after the due date has passed. You will receive a mark of zero if you have not officially submitted your assignment (and received a confirmation email) before the due date.

Your main program must be contained in a file called ImageViewer225.java; as mentioned in Section 4, you may not modify the provided ImageViewer225.java implementation. You may use additional files if needed by your solution (as long as the program can be invoked from the command line using the syntax in Section 5). Ensure that each submitted file contains a comment with your name and student number.

Ensure that all code files needed to compile and run your code in ECS 242 are submitted. Only the files that you submit through conneX will be marked. The best way to make sure your submission is correct is to download it from conneX after submitting and test it. You are not permitted to revise your submission after the due date, and late submissions will not be accepted, so you should ensure that you have submitted the correct version of your code before the due date. conneX will allow you to change your submission before the due date if you notice a mistake. After submitting your assignment, conneX will automatically send you a confirmation email. <strong>If you do not receive such an email, you did not submit the assignment. </strong>If you have problems with the submission process, send an email to the instructor <strong>before </strong>the due date.