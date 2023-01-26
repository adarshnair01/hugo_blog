+++
title = "Understanding Kalman Filters: A Practical Example"
description = "A blog  post explaining the beauty of Kalman Filters with an example"
tags = [
    "kalman",
    "filter",
    "gaussian",
    "control systems",
    "gps",
    "example",
    "estimation",
    "mathematics"
]
date = "2023-01-26"
categories = [
    "data science",
    "kalman filter",
    "algorithm",
    "mathematics"
]
menu = "main"
+++

Kalman filters are a powerful tool for estimating the state of a system based on a series of measurements. They are widely used in a variety of applications, including navigation, control systems, and signal processing. In this post, we will explore the concept of Kalman filters through a simple example of tracking a moving object using GPS measurements.

## Scenario
Our example scenario is a moving object that we want to track using GPS measurements. We know that the object's position and velocity are changing over time, and we want to estimate the true position and velocity of the object at each time step. To do this, we will use a Kalman filter algorithm.

## Kalman Filter Algorithm
The Kalman filter algorithm consists of two main steps: prediction and update. 

In the prediction step, we use a mathematical model of the system to predict the object's position and velocity at the next time step, based on the current position and velocity. 

In the update step, we use the GPS measurement of the object's position and velocity to update our estimate of the true position and velocity.

## Example
Let's walk through an example of how the Kalman filter algorithm works. 
At time k = 0, we have the first GPS measurement of x(0) = 10 meters and v(0) = 2 m/s. We also have an initial estimate of the object's position and velocity: x(0) = 10 meters and v(0) = 2 m/s. We can use the measurement and the estimate to update the estimate of the object's position and velocity: x(0) = (1-K) * x(0) + K * x(0) = (1-K) * 10 + K * 10 = 10 meters, v(0) = (1-K) * v(0) + K * v(0) = (1-K) * 2 + K * 2 = 2 m/s, where K is a Kalman gain.

At time k = 1, we have the second GPS measurement of x(1) = 12 meters and v(1) = 2.25 m/s. We also have the first estimate of the object's position and velocity: x(1) = 10 meters and v(1) = 2 m/s. We can use the measurement and the estimate to update the estimate of the object's position and velocity: x(1) = (1-K) * x(1) + K * x(1) = (1-K) * (10 + 2*dt) + (1-K) * 12 = 11.44 meters, v(1) = (1-K) * v(1) + K * v(1) = (1-K) * 2 + K * 2.25 = 2.19 m/s, where K is a Kalman gain and dt is the time step.

As the filter iterates, the estimated position and velocity will become more accurate, approaching the true position and velocity of the object. The Kalman filter uses a Gaussian distribution to model the uncertainty of the prediction and the measurement, and the updated estimate will be the center of this Gaussian distribution. The width of the distribution represents the uncertainty, and as the filter iterates, the width of the Gaussian distribution will decrease, indicating that the uncertainty of the estimate is decreasing.

The Kalman filter is a powerful tool for estimating the state of a system in the presence of noise and uncertainty. It is widely used in a variety of applications, including navigation, control systems, and signal processing.

However, the standard Kalman filter has its limitations. It assumes that the system being estimated is linear, which is not always the case. In non-linear systems, the Kalman filter can provide inaccurate estimates. This is where Cubature Kalman filter (CKF) comes into the picture. CKF is a variation of the standard Kalman filter that is designed to handle non-linear systems. It uses Gaussian cubature method to approximate the integral of the posterior probability density function, which allows it to handle non-linear functions of the state variables.

## Conclusion

We have explained the concept of Kalman filters through a simple example of tracking a moving object using GPS measurements. We have also discussed the limitation of standard Kalman filter and how Cubature Kalman filter can overcome it. The Kalman filter is a powerful tool for estimating the state of a system in the presence of noise and uncertainty. It is widely used in a variety of applications, including navigation, control systems, and signal processing.