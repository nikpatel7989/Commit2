# Commit2
I dhaval Patel 000741985, have not copied my work from any other source, this is my original work.

// do PascalCasing
/**
*avg = Average
*sd = Standarddeviation
*x = UserVAlue
*iceneg = IsNegative
*/

using System;
using System.Collections.Generic;

namespace Assignemnt4

{
    /**
     * Library of statistical functions using Generics for different statistical
     * calculations.
     * 
     * see http://www.calculator.net/standard-deviation-calculator.html
     * for sample standard deviation calculations
     *
     * @author Joey Programmer
     */

    public class A4
    {

        /**
         * <summary> 
         * Average method take two parameter 1. userValue and 2. incneg and calculates average
         * of that given values
         * </summary>
         * <param name="isNegative"> boolean parameter</param>
         * <param name="userValue">list of double values</param>
         * 
         * <returns average> returns the calculated average</returns>
         */
        public static double Average(List<double> UserValue, bool IsNegative)
        {
            // local variable to store addition of values that receive from another method
            double SumOfValue = Sum(UserValue, IsNegative);
            // counter variable to keep track of numbers
            int c = 0;
            // for loop to go through each value in the list and add to the variable 

            for (int i = 0; i < UserValue.Count; i++)
            {
                if (IsNegative || UserValue[i] >= 0)
                {
                    c++;
                }
            }
            if (c == 0)// throws an exception if no values in the list
            {
                throw new ArgumentException("no values are > 0");
            }
            return SumOfValue / c;
        }
        /**
         * <summary>
         * addition classs gets the double values from uservalue and isNegative and perform the addtion of the values
         * it also throws an exception if the userValue is empty
         * </summary> 
         * <param name="isNegative"> boolean variable</param>
         * <param name="userValue">list of double values</param>
         * <returns> sum of values in the list</returns>
         */

        public static double Sum(List<double> UserValue, bool IsNegative)
        {
            // throws an exception if the no values in the list
            if (UserValue.Count < 0)
            {
                throw new ArgumentException("x cannot be empty");
            }
            // variable to store addition of values
            double sum = 0.0;
            // for loop to add each value from the list to variable
            foreach (double val in UserValue)
            {
                if (IsNegative || val >= 0)
                {
                    sum += val;
                }
            }
            return sum;// returns the addition of values
        }
        /**
         * <summary>median method to find the median from given values. it throws an exception if size of an array is not greater than 0</summary>
         * <param name="data"> only contains the list of double values</param>
         * <returns> median value</returns>
         * 
         */
        public static double Median(List<double> data)
        {
            // throws and exception if values in the list is not greater than 0
            if (data.Count == 0)
            {
                throw new ArgumentException("Size of array must be greater than 0");
            }

            data.Sort();// sorts the data in the lsit

            // formula to find the meadian value
            double median = data[data.Count / 2];
            if (data.Count % 2 == 0)
                median = (data[data.Count / 2] + data[data.Count / 2 - 1]) / 2;

            return median;// return the median value
        }
        /**
         * <summary>calculates the standard devation of given values and throws an exception if the value is not greater than 1 </summary>
         * <param name="data"> list of double values</param>
         * <returns>calculated standard devation value</returns>
         */

        public static double StandardDeviation(List<double> data)
        {
            // throws and exception if size of an array is not greater than 1
            if (data.Count <= 1)
            {
                throw new ArgumentException("Size of array must be greater than 1");
            }

            int NumberOfCount = data.Count;// store the number of counts 
            double Sum = 0;// initialize the sum
            double Average = A4.Average(data, true);///finds the average

            for (int i = 0; i < NumberOfCount; i++)
            {
                double v = data[i];
                Sum += Math.Pow(v - Average, 2);// find the power value
            }
            double stdev = Math.Sqrt(Sum / (NumberOfCount - 1));
            return stdev;// return standard deviation value
        }
        // main method sends the data to each methods to calculate.
        // Simple set of tests that confirm that functions operate correctly
        static void Main(string[] args)
        {
            List<Double> testDataD = new List<Double> { 2.2, 3.3, 66.2, 17.5, 30.2, 31.1 };

            Console.WriteLine("The sum of the array = {0}", Sum(testDataD, true));// calls the sum method

            Console.WriteLine("The average of the array = {0}", Average(testDataD, true));//calls the average method

            Console.WriteLine("The median value of the Double data set = {0}", Median(testDataD));//calls the meadian method

            Console.WriteLine("The sample standard deviation of the Double test set = {0}\n", StandardDeviation(testDataD));// calls the standard deviation method
        }
    }
}
