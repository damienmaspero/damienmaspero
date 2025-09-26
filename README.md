# GitHub Profile - Dynamic Content via GraphQL API

This profile is powered by GitHub's GraphQL API to display dynamic information.

## GraphQL Query Example

Here's a GraphQL query to fetch user profile information:

```graphql
query GetUserProfile($username: String!) {
  user(login: $username) {
    login
    name
    bio
    location
    company
    websiteUrl
    avatarUrl
    followers {
      totalCount
    }
    following {
      totalCount
    }
    repositories(first: 10, orderBy: {field: UPDATED_AT, direction: DESC}) {
      totalCount
      nodes {
        name
        description
        stargazerCount
        forkCount
        primaryLanguage {
          name
          color
        }
        updatedAt
        url
      }
    }
    contributionsCollection {
      totalCommitContributions
      totalPullRequestContributions
      totalIssueContributions
    }
  }
}
```

## API Endpoint

- **GraphQL Endpoint**: `https://api.github.com/graphql`
- **Authentication**: Requires a GitHub Personal Access Token
- **Variables**: `{"username": "damienmaspero"}`

## Usage

To use this query, send a POST request to the GitHub GraphQL API:

```bash
curl -H "Authorization: bearer YOUR_TOKEN" \
     -X POST \
     -d '{"query": "query GetUserProfile($username: String!) { user(login: $username) { login name bio location company websiteUrl avatarUrl followers { totalCount } following { totalCount } repositories(first: 10, orderBy: {field: UPDATED_AT, direction: DESC}) { totalCount nodes { name description stargazerCount forkCount primaryLanguage { name color } updatedAt url } } contributionsCollection { totalCommitContributions totalPullRequestContributions totalIssueContributions } } }", "variables": {"username": "damienmaspero"}}' \
     https://api.github.com/graphql
```

This will return dynamic information about the GitHub profile including repositories, contributions, and profile details.
