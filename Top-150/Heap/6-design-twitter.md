[Design Twitter](https://leetcode.com/problems/design-twitter/)

# Intuition
To design a simplified version of Twitter, we need to store the tweets posted by each user and keep track of the users that each user follows. We can use a map to store the tweets of each user, where the key is the user ID and the value is a list of tweets. We can also use another map to store the followings of each user, where the key is the user ID and the value is a set of user IDs that the user follows.

To retrieve the news feed for a user, we need to get the most recent tweets from the user's own tweets and the tweets of the users they follow. We can use a priority queue to efficiently retrieve the top 10 most recent tweets.

# Approach
1. Use a map `userTweets` to store the tweets posted by each user, where the key is the user ID and the value is a list of tweets.
2. Use another map `followings` to store the users that each user follows, where the key is the user ID and the value is a set of user IDs.
3. Define a nested class `Tweet` to represent a tweet, which contains the tweet ID and the timestamp.
4. In the `postTweet` method:
   - If the user's list of tweets doesn't exist in `userTweets`, create a new list for the user.
   - Add the new tweet to the user's list of tweets, along with the current timestamp.
5. In the `getNewsFeed` method:
   - Create a priority queue `pq` to store the tweets, ordered by the timestamp in descending order.
   - Add all the tweets from the user's own list of tweets to the priority queue.
   - For each user that the user follows, add all their tweets to the priority queue.
   - Poll up to 10 tweets from the priority queue and add their IDs to the `newsFeed` list.
   - Return the `newsFeed` list.
6. In the `follow` method:
   - If the `followerId` and `followeeId` are the same, return.
   - If the `followerId` doesn't exist in `followings`, create a new set for the user.
   - Add the `followeeId` to the set of users that the `followerId` follows.
7. In the `unfollow` method:
   - If the `followerId` exists in `followings`, remove the `followeeId` from the set of users that the `followerId` follows.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
  - `postTweet`: O(1)
  - `getNewsFeed`: O(N log N), where N is the total number of tweets from the user and the users they follow.
  - `follow`: O(1)
  - `unfollow`: O(1)

* Space complexity: O(N)
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
  - The space complexity is O(N), where N is the total number of tweets and users in the system.

# Code
```java
class Twitter {
    private Map<Integer, List<Tweet>> userTweets;
    private Map<Integer, Set<Integer>> followings;
    private int timestamp;

    private class Tweet {
        int id;
        int time;

        Tweet(int id, int time) {
            this.id = id;
            this.time = time;
        }
    }

    public Twitter() {
        userTweets = new HashMap<>();
        followings = new HashMap<>();
        timestamp = 0;
    }

    public void postTweet(int userId, int tweetId) {
        if (!userTweets.containsKey(userId)) {
            userTweets.put(userId, new ArrayList<>());
        }
        userTweets.get(userId).add(new Tweet(tweetId, timestamp++));
    }

    public List<Integer> getNewsFeed(int userId) {
        PriorityQueue<Tweet> pq = new PriorityQueue<>((a, b) -> b.time - a.time);

        if (userTweets.containsKey(userId)) {
            pq.addAll(userTweets.get(userId));
        }

        if (followings.containsKey(userId)) {
            for (int followeeId : followings.get(userId)) {
                if (userTweets.containsKey(followeeId)) {
                    pq.addAll(userTweets.get(followeeId));
                }
            }
        }

        List<Integer> newsFeed = new ArrayList<>();
        while (!pq.isEmpty() && newsFeed.size() < 10) {
            newsFeed.add(pq.poll().id);
        }

        return newsFeed;
    }

    public void follow(int followerId, int followeeId) {
        if (followerId == followeeId) {
            return;
        }
        if (!followings.containsKey(followerId)) {
            followings.put(followerId, new HashSet<>());
        }
        followings.get(followerId).add(followeeId);
    }

    public void unfollow(int followerId, int followeeId) {
        if (followings.containsKey(followerId)) {
            followings.get(followerId).remove(followeeId);
        }
    }
}
```