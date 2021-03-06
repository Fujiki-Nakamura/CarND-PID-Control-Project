# Reflection
## 1. Describe the effect each of the P, I, D components
P (proportinal) component serves to keep a car to a reference trajectory. By minimizing CTE, P controller enables the car to have basic behaviors to keep track. However, P controller alone causes overshooting problems and the car can take oscillating behavior.

D (differential) component serves to controll car's behaviors smoothly. It considers the difference between the current CTE and the previous one (current CTE - previous CTE). When CTE decreaseis the value of current CTE - previous CTE becomes negative. By minusing the value from the P controller value, D controller decreases the CTE smoothly and solve the oscillating behavior by P controller.

I (integral) component serves to reduce biases. The biases can take several forms like steering drift. By considering the sum of the CTEs, I controller reduces the biases and makes PD controller even better.

## 2. Describe how the final hyperparameters were chosen
First of all, I started my experiment for tuning PID gains by (Kp, Ki, Kd) = (0.0, 0.0, 0.0). With these values, the car couldn't make an appropriate turn at the first left curve. That is reasonable because the car moved with steer value = 0.0.
For the car to keep track, I tuned Kp to 0.1 and make the car keep itself to the reference. Then, the car could make a turn at the first left curve.

However, the overshooting problem occurred and the car made an oscillating behavior. So, then I need to avoid it and tune Kd for the car to gracefully move around the track with oscillating. I tried Kd = 0.1, 0.2, 0.3, 0.4, 0.5, 0.7, 1.0. With Kd = 1.0, the car could make a turn at the second left curve and barely could make a turn at the third right curve. I continued tuning Kd to make a better turn at the 3rd curve and tried Kd = 1.2, 1.4, 1.6, 1.8, 2.0, 2.5, 3.0, 3.5, 4.0. With Kd = 4.0, the car improved the behavior but was slightly about to be out of the lane touching the lane lines at the 3rd curve.

Because continuing tuning Kd didn't seem to make improvements more, I tuned Ki then. Ki = 0.1, 0.05, 0.02, 0.01 produced large steering values and made the car out of the lane after the start. I tuned it to lower values and fould that Ki = 0.001 enabled the car to turn more gracefully at the 3rd curve without touching the lane lines. The behavior seemed pretty good but it seemed that the behavior could be better, so I continuced tuning. With Ki = 0.002, the car could make slightly better turns at the second and the third curves but oscillated at the first straight lane before the first curve. I wanted to avoid unneccesary oscillating behaviors so I setted on Ki = 0.001, and the final hyperparameters became (Kp, Ki, Kd) = (0.1, 0.001, 4.0).

