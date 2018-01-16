# Pigeon-Hole-Sorting
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using System.Text.RegularExpressions;

namespace Pigeonholesorting
{
    public class Pigeonhole
    {
        public void PHSorting(string filename)
        {
            try
            {
                using (StreamReader reader = new StreamReader(filename))
                {
                    string line = reader.ReadLine();
                    string[] alpha = line.Split(',');
                    bool check = false;
                    for (int i = 0; i < alpha.Length; i++)
                    {
                        check = Validate(alpha[i]);
                        if (check == true)
                        {
                            break;
                        }
                    }

                    if (check == true)
                    {
                        int[] array = Array.ConvertAll<string, int>(alpha, int.Parse);
                        int n = array.Length;
                        Fileinitial("Unsorted integer array is: ");
                        Output(array);
                        int min = Min(array);
                        int max = Max(array);
                        int Range = (max - min + 1);
                        int[] holes = new int[Range];
                        //Initializing the whole pigeonhole array to zero.
                        for (int i = 0; i < Range; i++)
                        {
                            holes[i] = 0;
                        }
                        //Now fill in the pigeonhole array
                        for (int i = 0; i < n; i++)
                        {
                            holes[array[i] - min] = holes[array[i] - min] + 1;
                        }

                        //Now place in the original array once again
                        int l = 0;
                        for (int i = 0; i < Range; i++)
                        {
                            for (; holes[i]-- > 0; )
                            {
                                array[l] = i + min;
                                l++;
                            }
                        }
                        Fileinitial("Sorted integer is: ");
                        Output(array);
                        return;
                    }
                    check = false;
                    for (int i = 0; i < alpha.Length; i++)
                    {
                        check = Checkchar(alpha[i]);
                        if (check == true)
                        {
                            break;
                        }
                    }
                    if (check == true)
                    {
                        char[] arr = Array.ConvertAll<string, char>(alpha, char.Parse);

                        int n = arr.Length;
                        int[] array = new int[n];
                        for (int i = 0; i < n; i++)
                        {
                            array[i] = Convert.ToInt32(arr[i]);
                        }
                        Fileinitial("Unsorted character array is:");
                        Outputc(arr);
                        int max = Max(array);
                        int min = Min(array);
                        int Range = (max - min + 1);
                        int[] holes = new int[Range];
                        //Initialize the pigeonhole array to 0
                        for (int i = 0; i < Range; i++)
                        {
                            holes[i] = 0;
                        }
                        //Now filling the pigeonhole array
                        for (int i = 0; i < n; i++)
                        {
                            holes[array[i] - min] = holes[array[i] - min] + 1;
                        }
                        int l = 0;
                        //Now convert it into the original array
                        for (int i = 0; i < Range; i++)
                        {
                            for (; holes[i]-- > 0; )
                            {
                                array[l] = i + min;
                                l++;
                            }
                        }

                        for (int i = 0; i < n; i++)
                        {
                            arr[i] = Convert.ToChar(array[i]);
                        }
                        Fileinitial("Sorted character array is:");
                        Outputc(arr);

                        return;
                    }
                    else
                    {

                        double[] array = Array.ConvertAll<string, double>(alpha, double.Parse);
                        Fileinitial("Unsorted double array is:");
                        Outputd(array);
                        int n = array.Length;
                        int[] result = new int[n];
                        double[] values = new double[n];
                        //For making it into rounded off values
                        for (int i = 0; i < n; i++)
                        {
                            result[i] = (int)Math.Ceiling(array[i]);
                        }

                        int min = Min(result);
                        int max = Max(result);
                        int Range = (max - min + 1);
                        int[] holes = new int[Range];
                        //Initialize the pigeonhole array to 0
                        for (int i = 0; i < Range; i++)
                        {
                            holes[i] = 0;
                        }
                        //Now filling the pigeonhole array
                        for (int i = 0; i < n; i++)
                        {
                            holes[result[i] - min] = holes[result[i] - min] + 1;
                        }
                        int l = 0;
                        //Now convert it into the original array
                        for (int i = 0; i < Range; i++)
                        {
                            for (; holes[i]-- > 0; )
                            {
                                result[l] = i + min;
                                l++;
                            }
                        }

                        double[] final = new double[n];
                        for (int i = 0; i < n; i++)
                        {
                            for (int j = 0; j < n; j++)
                            {
                                if (result[i] == (int)Math.Ceiling(array[j]))
                                {
                                    final[i] = array[j];
                                }
                            }
                        }
                        Fileinitial("Sorted double array is:");
                        Outputd(final);
                        return;
                    }
                    //    char[] array = Array.ConvertAll<string, char>(alpha, char.Parse); 
                    //arr = array.Select(i => Int32.Parse(i.ToString())).ToArray();
                }
            }
            catch (Exception e)
            {
                Console.WriteLine(e);
            }
        }
        public bool Validate(string lines)
        {
            return lines.All(char.IsNumber);
        }
        public bool Checkchar(string lines)
        {
            return lines.All(char.IsLetter);
        }
        public int Max(int[] arr)
        {
            int max = arr[0];
            for (int i = 0; i < arr.Length; i++)
            {
                if (max < arr[i])
                {
                    max = arr[i];
                }
            }
            return max;
        }
        public int Min(int[] arr)
        {
            int min = arr[0];
            for (int i = 0; i < arr.Length; i++)
            {
                if (min > arr[i])
                {
                    min = arr[i];
                }
            }
            return min;
        }
        public void Fileinitial(string n)
        {
            string filename = "C:\\Users\\computer world\\Desktop\\output file.txt";

            try
            {
                using (StreamWriter writer = File.AppendText(filename))
                {
                    writer.WriteLine("\n\nH");

                    writer.WriteLine(n);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine(e);
            }

        }
        public void Output(int[] array)
        {
            string filename = "C:\\Users\\computer world\\Desktop\\output file.txt";
            try
            {
                using (StreamWriter writer = File.AppendText(filename))
                {
                    //writer.WriteLine("\n");
                    for (int i = 0; i < array.Length; i++)
                    {
                        writer.Write("{0}, ", array[i]);
                    }
                    writer.WriteLine("\n");
                }
            }
            catch (Exception e)
            {
                Console.WriteLine(e);
            }
        }
        public void Outputc(char[] array)
        {
            string filename = "C:\\Users\\computer world\\Desktop\\output file.txt";
            try
            {
                using (StreamWriter writer = File.AppendText(filename))
                {
                    // writer.WriteLine("\n");
                    for (int i = 0; i < array.Length; i++)
                    {
                        writer.Write("{0}, ", array[i]);
                    }
                    writer.WriteLine("\n");
                }
            }
            catch (Exception e)
            {
                Console.WriteLine(e);
            }
        }
        public void Outputd(double[] array)
        {
            string filename = "C:\\Users\\computer world\\Desktop\\output file.txt";
            try
            {
                using (StreamWriter writer = File.AppendText(filename))
                {
                    //writer.WriteLine("\n");
                    for (int i = 0; i < array.Length; i++)
                    {
                        writer.Write("{0}, ", array[i]);
                    }
                    writer.WriteLine("\n");
                }
            }
            catch (Exception e)
            {
                Console.WriteLine(e);
            }

        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Pigeonhole pigeonhole = new Pigeonhole();
            string filename = "C:\\Users\\computer world\\Desktop\\input file.txt";
            pigeonhole.PHSorting(filename);
            Console.WriteLine("\nProgram has been finished. \nYou will find your required answer in a file named Output on your desktop.\n If not then please change the directory path of this file.");
            Console.ReadLine();
        }
    }
}
