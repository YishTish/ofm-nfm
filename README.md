Videos are available on a remote AZURE Storage BLOB. The access to the files is public, and to get to the right video, you will need to build the path according to the rules below:

main path:
https://hadasit.blob.core.windows.net/

Then, one of two types of tests:
ofm nfm

Each type has 4 tests:
    for ofm tests:
      obj1 obj2 obj3 obj4
    for nfm tests:
      Num1 Num2 Num3 Num4
Add "_video" to the test

Each test has 7 levels. The higher the number, the easier the test.
Start with "vid" and add one of the following:
24 18 13.5 10 7.5 5.5 4

each level has 20 files (according to files in the zipped folder) with avi suffix:
vid{filename}_at_{level}_Speed.avi

So the end result would be something like:
https://hadasit.blob.core.windows.net/nfm/Num1_video/24/vid918_at_24_Speed.avi


Stage 1 of the project:
Create the environment and set up the infrastructure. 
Download Angular and Material Desgin. You shouldn't need any js or css libraries, but if you need - do so. 
If you're familiar with gulp - set up gulp, with livereloa - easier for development.

Create a settings.js file. In it put the following settings (add to it if and when you need to):
1. Root directory of where the videos are. It is recommended that you use a local directory, within the path of the project (i.e. /files/video/...). 
2. An array of levels - var levels = [24, 18, 13.5, 10, 7.5, 5.5, 4];
3. A JSON object of the tests:
	numbers: {
		Num1: {	A: 129, 
			B: 168, 
			C: 205, 
			D: 253, ...},
		
		Num2: { A: 137, 
			B: 171, 
			C: 215, 
			D: 269, ...},
		...
	};
	objects: {
		Obj1: {
			A: 'apple', 
			B: 'binoculars', 
			C: 'bow', 
			D: 'candy'...},
		
		Obj2: {
			A: 'airplane', 
			B: 'anchor', 
			C: 'decanter', 
			D: 'elefant', ...},
		...
	};

Stage 2:
Create the main page (for now) for the application. It should be a simple form with Material-style buttons. 
Form content:
Name of patient (text box)
Test type (two buttons to select - Objects or Numbers)
Test number (radio or select box - 1-4)
Start test - disabled until everything else has been filled.

Stage 3:
Once all the fields have been filled, and the Start Test button was pressed, open a modal that darkens the rest of the screen. The test begins.

Stage 4:
Write a service that generates the parameters for the test.
a. Collects the objects/numbers that are going to be displayed - and shuffles them: e.g. testElements = shuffle(objects.Obj2);
b. Sets the level of the test at levels[0];
c. Creates a "test sheet". The test sheet is a JSON object that consists of the test displayed, the level in which it was identified, and the score given.

Stage 5:
Run the test. 
For each element in testElements, get the video clip (write a service that builds the path based on instructions given above. You send the test type, name, and level, and get a full path in return), and show it in the modal.
When the clip is over, show a row containing the key of the movie-clip (for Num1 clip 129 show A, for Obj2 clip 'elefant' show D) and a password text box for the tester to write if the answer was right or wrong (we will modify it later so that the numbers show only a text box. We will know if the patient was right or wrong. For objects we need manual input).

