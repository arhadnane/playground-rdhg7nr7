# Welcome!

Nuggets numbers: 

using System;
internal class NestedLoop
    {

private static void Main()
{
    
    Nuggets_numbers();

    Console.ReadLine();
}

 internal static void Nuggets_numbers()
    {
        List<int> nuggets = new List<int> {600,91,205};
        int max = 3*nuggets.Max();
        bool[] isMcNuggetNumber = new bool[max + 1];

        var data2 = new List<List<int>>();
        foreach (int coef in nuggets)
        {
            data2.Add(Enumerable.Range(0,max/coef).Select(x => x*coef).ToList<int>());
        }

        if (findGCD(nuggets.ToArray(), nuggets.Count) != 1)
        {
            Console.WriteLine("NA : Infinity (-1)");
            return;
        }

        foreach (var item in IterateDynamicLoop(data2).Select(x => x.Sum()))
        {
            if (item <= max)
            {
                isMcNuggetNumber[item] = true;
            }
        }

        for (int mnnCheck = isMcNuggetNumber.Length - 1; mnnCheck >= 0; mnnCheck--)
        {
            if (!isMcNuggetNumber[mnnCheck])
            {
                Console.WriteLine($"Largest non-McNuggett Number less than {max}: " + mnnCheck.ToString());
                break;
            }
        }

            //Console.ReadLine();
    }

 private static IEnumerable<IEnumerable<T>> IterateDynamicLoop<T>(IList<List<T>> data)
        {
            var count = data.Count;

            var loopIndex = count - 1;
            var counters = new int[count];
            var bounds = data.Select(x => x.Count).ToArray();

            do
            {
                yield return Enumerable.Range(0, count).Select(x => data[x][counters[x]]);
            } while (IncrementLoopState(counters, bounds, ref loopIndex));
        }

        private static bool IncrementLoopState(IList<int> counters, IList<int> bounds, ref int loopIndex)
        {
            if (loopIndex < 0)
                return false;

            counters[loopIndex] = counters[loopIndex] + 1;

            var result = true;

            if (counters[loopIndex] >= bounds[loopIndex])
            {
                counters[loopIndex] = 0;
                loopIndex--;
                result = IncrementLoopState(counters, bounds, ref loopIndex);
                loopIndex++;
            }

            return result;
        }

        private static int gcd(int a, int b)
        {
            if (a == 0)
                return b;
            return gcd(b % a, a);
        }

        private static int findGCD(int[] arr, int n)
        {
            int result = arr[0];
            for (int i = 1; i < n; i++)
            {
                result = gcd(arr[i], result);

                if (result == 1)
                {
                    return 1;
                }
            }

            return result;
        }

    }

# Advanced usage

If you want a more complex example (external libraries, viewers...), use the [Advanced C# template](https://tech.io/select-repo/386)
