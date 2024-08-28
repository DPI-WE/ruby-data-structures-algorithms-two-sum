# Array Pair Sum ➕

### [Here is a video for this lesson](https://www.youtube.com/watch?v=0tu0F9zrBtY)

## The problem
Write a program that
- takes an array of integers (array) and a target integer sum (sum)
- finds all the pairs of integers in the array that when added together equals the target sum
- return array of integer pairs (eg [[2,3], [1,4]]).

## Understand the Problem
Before tackling the main problem, let's warm up with a simpler task to get you comfortable with the concept of searching for pairs in an array.

- Consider the array [1, 2, 3] and a target sum of 4. Can you find a pair of numbers in this array that adds up to the target sum? 
- (1, 2)
  - Not quite. The sume of 1+2=3. We need it to sum to 4.
- (1, 3)
  - Yes, the pair (1, 3) adds up to 4.
- (4)
  - Not quite right. Re-read the previous sections and try again.
{: .choose_best #problem_example title="Consider the array [1, 2, 3] and a target sum of 4" points="1" answer="[2]" }

Keep this process in mind as we move to the coding problem. Make sure your program works with the randomly sampled arrays and sums below, then get the tests to pass. Remember, the goal is not just to find the solution but to understand the process and improve your problem-solving skills. Take your time, experiment with different approaches, and see what works best for you.

## Think Aloud
Remember, interviewers want to see how you approach problems. Verbalize your thought process and write pseudocode as you break down the problem and explore solutions. It’s okay to start with a simpler, less efficient solution. You can always refine it later.

## Test your code

```ruby
arrays = [
  [1, 2, 3, 4, 5],
  [0, -1, 2, -3, 1],
  [11, -4, 7, 8, -10]
]
sums = [5, -2, 3]
array = arrays.sample
sum = sums.sample
# write your program using this method
def two_sum(array, sum)

end

puts two_sum(array, sum)
```
{: .repl #array_pair_sum title="Array Pair Sum" readonly_lines="[1,2,3,4,5,6,7,8,9,10,12]"}

```ruby
describe "Array Pair Sum" do
  it "finds pairs that sum to 5 in the array [1, 2, 3, 4, 5]" do
    result = two_sum([1, 2, 3, 4, 5], 5)
    expected = [[1, 4], [2, 3]]
    expect(result.map(&:sort)).to match_array(expected.map(&:sort))
  end
end
```
{: .repl-test #array_pair_sum_test_1 for="array_pair_sum" title="Array Pair Sum finds pairs that sum to 5" points="1"}

```ruby
describe "Array Pair Sum" do
  it "finds pairs that sum to -2 in the array [0, -1, 2, -3, 1]" do
    result = two_sum([0, -1, 2, -3, 1], -2)
    expected = [[-3, 1]]
    expect(result.map(&:sort)).to match_array(expected.map(&:sort))
  end
end
```
{: .repl-test #array_pair_sum_test_2 for="array_pair_sum" title="Array Pair Sum finds pairs that sum to -2" points="1"}

```ruby
describe "Array Pair Sum" do
  it "finds pairs that sum to 3 in the array [11, -4, 7, 8, -10]" do
    result = two_sum([11, -4, 7, 8, -10], 3)
    expected = [[-4, 7]]
    expect(result.map(&:sort)).to match_array(expected.map(&:sort))
  end
end
```
{: .repl-test #array_pair_sum_test_3 for="array_pair_sum" title="Array Pair Sum finds pairs that sum to 3" points="1"}

```ruby
describe "Array Pair Sum" do
  it "efficiently handles a very large array, suggesting O(n) time complexity" do
    large_array = Array.new(100000) { rand(-10000..10000) }
    target_sum = rand(-20000..20000)
    start_time = Time.now
    result = two_sum(large_array, target_sum)
    end_time = Time.now
    expect(end_time - start_time).to be < 1 # Test should complete quickly for an O(n) solution
  end
end
```
{: .repl-test #array_pair_sum_test_4 for="array_pair_sum" title="Array Pair Sum efficiently handles a very large array, suggesting O(n) time complexity" points="1"}

## Tips and Clues for Solving the Problem

- **Nested Loops**: One way to approach this is by using two nested loops to check every possible pair of numbers in the array. This is straightforward but not the most efficient.
- **Hash**: A more efficient method involves using a [hash](https://ruby-doc.org/3.2.2/Hash.html). As you iterate through the array, check if the complement (target sum - current number) exists in the hash. If it does, you've found a pair. If not, add the current number to the hash and move on.

<aside>
  There are multiple terms used to describe this key-value data structure: Dictionary, Map, Hash Map, Hash Table, etc. For our purposes, we will simply use the term Hash.
</aside>

- **Edge Cases**: Don't forget to consider edge cases. What happens if the array is empty or contains only one element?
- **Duplicates**: How will your program handle duplicate pairs or numbers? Make sure to test your solution against such cases.

## Quiz

- What does a hash primarily provide in algorithm problems?
- A way to store data for quick sorting
  - Incorrect. While a hash can improve some operations, they are not primarily used for sorting. Consider what makes a hash unique in managing data.
- A method for rapid data retrieval based on key
  - Correct! Hashes excel at fast data access using keys (time complexity of O(1)), making them ideal for situations where quick lookup of values is needed.
- A tool for data encryption
  - Incorrect. Hashes are used for data storage and retrieval, not encryption. Think about how data is accessed in a hash.
- A structure for organizing hierarchical data
  - Incorrect. Hashes are not inherently hierarchical. They are better suited for key-value pair storage. Consider the flat nature of hash storage.
{: .choose_best #why_hash title="What does a hash primarily provide in algorithm problems?" points="1" answer="2" }

- In Ruby, which method can be used to iterate over each element in an array?
- `each`
  - Correct, but there's more. The `each` method does allow iteration over each element, but it's not the only method that can do this.
- `map`
  - Correct, but keep in mind there's more. `map` is used for transforming elements in an array through iteration, but it's not the only method for iteration.
- `filter`
  - Correct, but there's a broader perspective. While `filter` (in Ruby, often used as `select`) iterates over elements to filter them, it's not the only iterative method.
- All of the above
  - Correct! Each of these methods (`each`, `map`, and `filter`/`select`) can be used to iterate over elements in an array, each serving different purposes in the process.
{: .choose_best #iterators title="Which method can be used to iterate over each element in an array?" points="1" answer="4" }

- Which approach is most efficient for finding pairs in an array that sum to a specific value?
- Using two nested loops to check every pair
  - Close. This could work, but is O(n^2) time complexity. Is there a more efficient approach?
- Sorting the array and then checking each pair for the sum
  - Close. This could work, but is O(n log n) time complexity. Is there a more efficient approach?
- Using a hash to store and check for complements
  - Correct! A hash is generally more efficient for this specific problem type, especially in cases where the array does not need to be sorted for any other purpose.
{: .choose_best #most_efficient_method title="Which approach is most efficient for finding pairs in an array that sum to a specific value?" points="1" answer="3" }


<!-- TODO: follow on short answer question -->
<!-- Explain how a hash can be used to find a pair of numbers in an array that sum up to a given target. Please explain the time and space complexity for this approach.

Sample Answer: A hash can be used to track the elements we've seen as we iterate through the array. For each element, we calculate its complement by subtracting the element from the target sum. We then check if this complement is already in our hash. If it is, we've found a pair that sums up to the target. If not, we add the current element to the hash and continue. This allows for efficient lookups and avoids the need for nested loops, significantly reducing the time complexity from O(n^2) to O(n). -->

## Conclusion
In this lesson, we've explored the problem of finding pairs in an array that sum to a given target. By breaking down the problem, considering various strategies for approaching it, and applying key programming concepts, we've equipped you with the tools to tackle similar challenges.

## Resources
- [leetcode](https://leetcode.com/problems/two-sum)
