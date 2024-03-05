# p4 - Slow Arc System

## Group 1
- Tyler Pham
- Yan Shen
- Sulekha Abas
- Siham Ali

## Video Demo
YouTube link: `https://youtu.be/wA-Cn4oJGWs`

## Steps to Run Slow Arc System
To run the Arc System, we must first install the necessary requirements. Then, we can run the main module.
1. `pip install -r requirements.txt`
2. `python3 -m src.main`

## Testing
The repository contains unit tests and end-to-end integration test scenarios within `src/tests/`. The unit test are within `src/tests/unit_test.py` and the end-to-end integration tests are in `src/tests/integration_test.py`.

#### Run All Tests:
`python3 -m pytest src/tests/ -v`

#### Run Unit Tests:
`python3 -m pytest src/tests/unit_test.py -v`

#### Run End-to-end Integration Tests:
`python3 -m pytest src/tests/integration_test.py -v`

## CSV Data File Format
Here is the file format for the pitch data files within `src/data/`:

Line 1 : Front-close corner (x,y)\
Line 2 : Back-close corner (x,y)\
Line 3 : Point (x,y)\
Line 4 : Back-far corner (x,y)\
Line 5 : Front-far corner (x,y)\
Line 6 : Shoulder 1 (x,y)\
Line 7 : Shoulder 2 (x,y)\
Line 8 : Knee 1 (x,y)\
Line 9 : Knee 2 (x,y)\
Line 10+ : Pitch data (timestamp, ball-center-x, ball-center-y, ball-left-x, ball-left-y, ball-right-x, ball-right-y)

The (x,y) axes from the sensor are a little odd. (0,0) is the top left corner of the screen, instead of the bottom left like we would like. The y-coordinate will increase as the pitch comes down. The first five lines are the coordinates of the five points of the plate, moving from front-left corner counter-clockwise. The next four lines capture the coordinates of both shoulders and both knees of the batter. The remaining lines give the actual pitch data: a timestamp, coordinates for the center of the ball, and then coordinates for both the left and right sides of the ball through the center. Use the left/right sides of the ball to determine it's width in pixels. Compare the known size of the ball, the known size of both sides of the plate, and the pixel widths of each to determine where the ball is in terms of depth.

## Visualizations
For each pitch, there is a side view and a front view plotted on a graph. The side view shows the strike zone and the plate, along with the path of the ball. The side view is pretty self-explanatory, except that the y-coordinates are all inverted (-y) in order to give us something that looks like what we expect. The front view is the result of doing some inches/pixel calculations (and then scaling at a factor of 10x to be able to see it more easily)