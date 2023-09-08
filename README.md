# Twitter-Non-Reciprocal_Follower_Unsubscribe_32
This script allows you to automatically unfollow non-reciprocal followers on Twitter. 
Non-reciprocal followers are users who follow you, but you are not following them back. With this script, you can clean up your follow list by removing users who are not actively engaging with you.

# Twitter_API_credentials
consumer_key = 'YOUR_CONSUMER_KEY'
consumer_secret = 'YOUR_CONSUMER_SECRET'
access_token = 'YOUR_ACCESS_TOKEN'
access_token_secret = 'YOUR_ACCESS_TOKEN_SECRET'

# Authenticate to Twitter API
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth)

# Get followers
followers = set(api.followers_ids())
friends = set(api.friends_ids())

# Find non-reciprocal followers
non_reciprocal = followers - friends

# Unfollow non-reciprocal followers:
for user_id in non_reciprocal:
    try:
        api.destroy_friendship(user_id)
        print(f"Unfollowed user with ID: {user_id}")
    except tweepy.error.TweepError as e:
        print(f"Error unfollowing user with ID {user_id}: {e}")
