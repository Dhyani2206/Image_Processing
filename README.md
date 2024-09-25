**Tools Used:** Anaconda (Jupyter Notebook), LabelMe 
**Skills Gained:** Annotation, Semantic Segmentation, Filters, Masking and Unmasking Images, Labelling Images
**About Annotation:**
- Annotation is the process of adding supplementary information or labels to data, such as text, images, or videos, to enhance its understanding and context. It aids machine learning algorithms in recognizing patterns, training models, and improving accuracy by providing human-verified ground truth. Annotations are crucial for tasks like natural language processing and computer vision.
- There are various annotation tools but in the tasks done ‘LabelMe Tool’ is used. It is an opensource graphical image annotation tool used for creating labeled datasets for computer vision tasks. LabelMe allows users to draw bounding boxes and polygons around objects of interest in images. It also supports semantic segmentation by labeling individual pixels in an image.
**Tasks:**
1. AOI to JSON:
- In this particular task the images with product in it are converted to Json images and are also labelled as product.
- Process: Take the input image and load it -> Convert the image to grayscale and apply thresholding -> Find the contours by applying filters as per requirement -> Draw contours and convert the file into Json format by applying the format of Json 
2. AOI to JSON - Oval Capsules and Bottles:
- This python code is developed specially for products who are oval or possess bottle like shape.
- The hyperparameters tunned for this are as follows:	
   - As oval like shape has minimum 6 vertices therefore ‘len(approx) >= 6’
   - Here approx = cv2.approxPolyDP(cnt, 0.002 * perimeter, True) , where approxPolyDP approximates a curve or a polygon with another curve/polygon with less vertices so that the distance between them is less or equal to the specified precision.
3. AOI to JSON - Outer Boundaries:
- This python code is developed specially for drawing the outer boundaries of products.
- The hyperparameters tunned for this are as follows:	
   - As we have to draw the outer boundaries we don’t need to tune many parameters, we have to only set the threshold value, i.e., area which I have set as area >  400
4. Drawing Rectangles:
- In this task we need to draw rectangles around the polygons annotated so as input we need to provide Json and image file.
- To draw rectangles we need to use minAreaRect for finding the minimum area rotate rectangle which takes input of 2D point set and returns 2D Box structure containing height, width, centre(points) and angle of rotation.
- After that we need to crop that polygon by taking the image and points in the consideration. boundingRect is used to draw a proper rectangle around the binary image through this we can highlight the region of interest.
5. Cropping Out:
- In this task we need to draw rectangles around the polygons annotated as well as we need crop out the polygons so as input we need to provide Json and image file.
- All the process is almost same as drawing rectangle boxes the extra step we need to perform is that crop out the polygon by using points of max height and width.
- cropped_image = image[max(0, y):y+h, max(0, x):x+w]
6. Masking Images:
- For this task, the objective is to extract contours from the images in the dataset. To achieve this, follow the steps outlined below: 
-> Load the image.
-> Create a new image with a white background.
-> Iterate through each shape in the JSON file.
-> Convert the points to integers.
-> Draw the polygon on the new image.
-> Copy the original image within the bounds of the polygon.
-> Save the cropped image.
7.Flipping The Images:
- The objective of this task is to mirror the images along with their corresponding JSON files. This can be accomplished through three methods:
(i) Horizontal flipping: This involves flipping the images from left to right along the x-axis.
(ii) Vertical flipping: Here, the images are flipped from top to bottom along the y-axis.
(iii) Counter-clockwise rotation by 90 degrees: In this approach, the coordinates of the 	JSON file are swapped, interchanging the x and y values, and saved in new 	variables. This results in a 90-degree rotation of the image.
