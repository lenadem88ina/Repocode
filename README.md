# Repocode
import os
import requests

def create_github_repo(repo_name, token):
  """Creates a new GitHub repository.

  Args:
    repo_name: The name of the new repository.
    token: Your GitHub personal access token.

  Returns:
    True if the repository was created successfully, False otherwise.
  """

  url = f"https://api.github.com/user/repos"
  headers = {
    "Authorization": f"token {token}",
    "Accept": "application/vnd.github+json"
  }
  data = {"name": repo_name}

  response = requests.post(url, headers=headers, json=data)

  if response.status_code == 201:
    print(f"Repository '{repo_name}' created successfully!")
    return True
  else:
    print(f"Error creating repository: {response.text}")
    return False

def get_github_token():
  """Gets your GitHub personal access token from the environment variable."""
  return os.getenv("GITHUB_TOKEN")

if __name__ == "__main__":
  repo_name = input("Enter the name of the new repository: ")
  token = get_github_token()

  if token:
    create_github_repo(repo_name, token)
  else:
    print("Error: GitHub token not found. Please set the GITHUB_TOKEN environment variable.")
