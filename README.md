# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`.

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

### Rubric

#### Compilation

1. Your code should compile.
   Based on the steps provided above, following output was received for build.


        Jinays-MacBook-Air:build jinay$ cmake ..
        -- The C compiler identification is AppleClang 9.1.0.9020039
        -- The CXX compiler identification is AppleClang 9.1.0.9020039
        -- Check for working C compiler: /Library/Developer/CommandLineTools/usr/bin/cc
        -- Check for working C compiler: /Library/Developer/CommandLineTools/usr/bin/cc -- works
        -- Detecting C compiler ABI info
        -- Detecting C compiler ABI info - done
        -- Detecting C compile features
        -- Detecting C compile features - done
        -- Check for working CXX compiler: /Library/Developer/CommandLineTools/usr/bin/c++
        -- Check for working CXX compiler: /Library/Developer/CommandLineTools/usr/bin/c++ -- works
        -- Detecting CXX compiler ABI info
        -- Detecting CXX compiler ABI info - done
        -- Detecting CXX compile features
        -- Detecting CXX compile features - done
        -- Configuring done
        -- Generating done
        -- Build files have been written to: /Users/jinay/workspace/git-repo/udacity/term2/CarND-PID-Control-Project/build

        Jinays-MacBook-Air:build jinay$ make
        Scanning dependencies of target pid
        [ 33%] Building CXX object CMakeFiles/pid.dir/src/PID.cpp.o
        [ 66%] Building CXX object CMakeFiles/pid.dir/src/main.cpp.o
        /Users/jinay/workspace/git-repo/udacity/term2/CarND-PID-Control-Project/src/main.cpp:57:28: warning: unused variable 'speed' [-Wunused-variable]
                            double speed = std::stod(j[1]["speed"].get<std::string>());
                                  ^
        /Users/jinay/workspace/git-repo/udacity/term2/CarND-PID-Control-Project/src/main.cpp:58:28: warning: unused variable 'angle' [-Wunused-variable]
                            double angle = std::stod(j[1]["steering_angle"].get<std::string>());
                                  ^
        /Users/jinay/workspace/git-repo/udacity/term2/CarND-PID-Control-Project/src/main.cpp:104:22: warning: lambda capture 'h' is not used
              [-Wunused-lambda-capture]
            h.onConnection([&h](uWS::WebSocket<uWS::SERVER> ws, uWS::HttpRequest req) {
                            ^
        /Users/jinay/workspace/git-repo/udacity/term2/CarND-PID-Control-Project/src/main.cpp:108:25: warning: lambda capture 'h' is not used
              [-Wunused-lambda-capture]
            h.onDisconnection([&h](uWS::WebSocket<uWS::SERVER> ws, int code, char *message, size_t length) {
                                ^
        4 warnings generated.
        [100%] Linking CXX executable pid
        ld: warning: directory not found for option '-L/usr/local/Cellar/libuv/1*/lib'
        [100%] Built target pid

#### Implementation

1. The PID procedure follows what was taught in the lessons.
   Based on the `TODO` provided in code, appropriate implementation as per the lesson are implemented. Modified files are `src/main.cpp` and `src/PID.cpp`

   For ``PID`` features and error calculations implementation is part of `src/PID.cpp`.

#### Reflection

1. Describe the effect each of the P, I, D components had in your implementation.

   -  Proportional portion of controller tries to steer the car towards the center line, if used along, the car overshoots easily to center line and goes out of the track.
   -  Integral portion of controller tries eliminate possible bias on controlled system that could prevent the error to be eliminated. If used along, it makes car to go in circles.
   -  Differential portion of controller tries to counteract to effect of proportional portion tend to overshoot center line by smoothing the approach to it.
2. Describe how the final hyperparameters were chosen.
   Parameters were chosen manually with trial and error. With initial values, tried make sure car drive with straight line, then add the proportional portion and car start going forward on road and starts following road but fails to recover from trajectory line. After applied differential to try overcome the overshoot of center line. The integral part only moved car out of the road, so it stayed zero. Car drove entire track without going out of the road with parameters set. Final parameters are

        P: 1.5  I: 0.0  D: 2.5

#### Simulation

1. The vehicle must successfully drive a lap around the track.
   Vehicle has successfully completed lap without going out of the road with set parameters.