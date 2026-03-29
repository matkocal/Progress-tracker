# Progress-tracker
Simple graphical progress tracker. 

1. Program reads the file `progress_values.json` on start and loads the values to a dictionary variable `progress_values`

2. Program reads a new data pair from console:

   - date in format YYYY-MM-DD
   - value in range 1-100

3. Program adds new data pair, add it to variable `progress_values` and saves it to the existing values in `progress_values.json` and saves it

4. Program create a canvas and draws a graph where X represents dates and Y represents values and links values points

