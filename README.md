# people-you-might-know

Implementation of a simple `People-You-Might-Know` social network friendship recommendation  algorithm using PySpark. The key idea is that if two people have a lot of mutual friends, then the system should recommend that they connect with each other.

## Input

[`Friends.txt`](Friends.txt)

The input file contains the adjacency list and has multiple lines in the following format:
```
<User><TAB><Friends>
```

Here, `<User>` is a unique integer ID corresponding to a unique user, and `<Friends>` is a comma-separated list of unique IDs corresponding to the friends of the user with the unique ID `<User>`. Note that the friendships are mutual: if A is friends with B then B is also friends with A. The data provided is consistent with that rule.

## Algorithm

Calculate a ‘friendship score’ to determine the ordering of the recommended IDs via the number of mutual friends.

`<Recommendations>` is a comma-separated list of unique IDs corresponding to the algorithm’s recommendation of people that <User> might know ordered by the decreasing number of mutual friends.

For example, the score for `user2` as a friend of `user1` is 1+1+1: each common friend contributes 1 to the score assuming there are 3 mutual friends between `user2` and `user1`.

For each user U, the algorithm recommends N = 10 users who are not already friends with U, but have the largest number of mutual friends or have the highest influence score.

Even if a user has fewer than 10 second-degree friends, output all of them in decreasing order of the number of mutual friends or decreasing order of the influence score. If a user has no friends, you can provide an empty list of recommendations. If there are multiple users with the same number of mutual friends or the same influence score, ties are broken by ordering them in a numerically ascending order of their user IDs.

## Output

The output should contain one line per user in the following format
```
<User><TAB><Recommendations>
```
where `<User>` is a unique ID corresponding to a user and `<Recommendations>` is a comma-separated list of unique IDs corresponding to the algorithm’s recommendation of people that `<User>` might know.

## Future Work

We can also calculate the influence score to determine the ordering of the recommended IDs via the influence of the common friend.

`<Recommendations>` is a comma-separated list of unique IDs corresponding to the algorithm’s recommendation of people that `<User>` might know ordered by the decreasing influence score for a given recommended user.

Here, the influence score for `user2` for being recommended to `user1` is

```math
\frac{1}{𝑛𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐹𝑟𝑖𝑒𝑛𝑑𝑠(𝑓1)} + \frac{1}{𝑛𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐹𝑟𝑖𝑒𝑛𝑑s(𝑓2)} + \frac{1}{𝑛𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐹𝑟𝑖𝑒𝑛𝑑𝑠(𝑓3)}
```
where `numberOfFriends(f)` is the number of friends that `f` has, assuming `user2` has three friends in common with `user1`. In other words, each friend `f` of `user2` has a total influence score of 1 to contribute divided by the total number of `f`'s friends, in order to weigh the friends in common by their influence.

## Collaborators

- Manasa Devarapalli - [@dmanasa6](https://github.com/dmanasa6)

We stumbled upon this problem during a random discussion and decided to implement it.

[people-you-might-know.ipynb](people-you-might-know.ipynb) is the Jupyter notebook containing the code.

## License

Creative Commons Attribution (CC BY)
