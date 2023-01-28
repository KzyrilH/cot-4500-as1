# cot-4500-as1
Assignment 1
#Kzyril Hubilla
#COT 4500 (Parra)
#src/main/Assignment1.py

import math

#1) Use double precision, calculate the resulting values (format to 5 decimal places) 
    #a) 010000000111111010111001 
#2) Repeat exercise 1 using three-digit chopping arithmetic 
#3) Repeat exercise 1 using three-digit rounding arithmetic 
#4) Compute the absolute and relative error with the exact value from question 1 and its 3 digit rounding
#5) What is the minimum number of terms needed to computer f(1) with error < 10-4? 
#6) Determine the number of iterations necessary to solve f(x) = x3 + 4x2 – 10 = 0 with accuracy 10-4 using a = -4 and b = 7. 
    #a) Using the bisection method 
    #b) Using the newton Raphson method 

def double_precision(binary_string):
    decimal = int(binary_string, 2)
    decimal = float(decimal)
    return round(decimal, 5)

def three_digit_chopping(binary_string):
    decimal = int(binary_string, 2)
    decimal = decimal / 1000
    return round(decimal, 5)

def three_digit_rounding(binary_string):
    decimal = int(binary_string, 2)
    decimal = round(decimal / 1000, 3)
    return round(decimal, 5)

def error(exact, approx):
    absolute = abs(exact - approx)
    relative = absolute / exact
    return absolute, relative

def bisection(a, b, tolerance):
    iterations = 0
    while (b - a) / 2 > tolerance:
        c = (a + b) / 2
        f_a = a**3 + 4*a**2 - 10
        f_c = c**3 + 4*c**2 - 10
        if f_a * f_c < 0:
            b = c
        else:
            a = c
        iterations += 1
    return iterations

def newton_raphson(x, tolerance):
    iterations = 0
    while True:
        f_x = x**3 + 4*x**2 - 10
        f_prime_x = 3*x**2 + 8*x
        x_new = x - f_x / f_prime_x
        if abs(x_new - x) < tolerance:
            break
        x = x_new
        iterations += 1
    return iterations

if __name__ == "__main__":
    binary_string = "010000000111111010111001"
    decimal = int(binary_string, 2)
    double_precision_result = double_precision(binary_string)
    three_digit_chopping_result = three_digit_chopping(binary_string)
    three_digit_rounding_result = three_digit_rounding(binary_string)
    absolute_error, relative_error = error(decimal, three_digit_rounding_result)
    bisection_iterations = bisection(-4, 7, 0.0001)
    newton_raphson_iterations = newton_raphson(4, 0.0001)

#print statements for questions

    print("Double precision result: ", double_precision_result)
    print("Three digit chopping result: ", three_digit_chopping_result)
    print("Three digit rounding result: ", three_digit_rounding_result)
    print("Absolute error: ", absolute_error)
    print("Relative error: ", relative_error)
    print("Bisection method iterations: ", bisection_iterations)
    print("Newton Raphson method iterations: ", newton_raphson_iterations)
