## DAY 01 - Trebuchet?!

Advent of Code this year has started with a good parsing problem. In this page, I'm specifically talking about the second part of the problem. 
So, you're given a list of 1000 strings and your goal is to detect all the numbers either in numeric form (ex. '2') or spelled out (ex. 'two'). 
Your function is expected to return an integer comprising of first and last digits detected in each string.

```
two1nine -> 29
eightwothree -> 83
abcone2threexyz -> 13
xtwone3four -> 24
4nineeightseven2 -> 42
zoneight234 -> 14
7pqrstsixteen -> 76
```
It seems like a job for regular expressions but that's not what this page is about. Initially, I solved the problem using regex and challenged myself to do it again without using regex. 
My first thought was to use sliding windows (although now I feel like two pointer technique is a better alternative). After a few tries, I finally got the code running. 
And no surprise, it was inefficient. It was ~10x slower than the regex implementation. But my goal was a no-regex implementation, I succeded and I'm leaving improvements to the future. 
```python
nums = {'one':'1', 'two':'2', 'three':'3', 'four':'4', 'five':'5',
                 'six':'6', 'seven':'7', 'eight':'8', 'nine':'9'}   

def solve(s:str) -> int:
    window_start:int = 0
    window_end:int = 1
    num_list:list = []

    while window_start < len(s):
        curr:list = s[window_start:window_end]
        
        if curr in nums.keys() or curr in nums.values():
            num_list.append(nums[curr] if curr in nums.keys() else curr)
            window_start = window_end - 1
           
        window_end += 1

        if (window_end - window_start) > 5 or window_end > len(s):
            window_start += 1
            window_end = min(window_start + 1, len(s))
        
    result = int(num_list[0] + num_list[-1])
    return result
```
