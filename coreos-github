import sys
import argparse
from github import Github

def add_default_hooks(repo):
    add_irc_hook(repo)
    add_email_hook(repo)

def add_email_hook(repo):
    events = [
      "commit_comment",
      "issue_comment",
      "issues",
      "pull_request",
      "pull_request_review_comment",
      "push"
    ]
    config = {
        'address': 'coreos-dev-notifications@googlegroups.com',
    }

    repo.create_hook('email', config, events, True)

def add_irc_hook(repo):
    events = [
      "commit_comment",
      "issue_comment",
      "issues",
      "pull_request",
      "pull_request_review_comment",
      "push"
    ]
    config = {
        'server': 'irc.freenode.net',
        'port': '6667',
        'room': '#coreos',
        'nick': 'coreos-gh',
        'message_without_join': '1',
        'notice': '1'
    }

    repo.create_hook('irc', config, events, True)

def delete_all_hooks(repo):
    hooks = repo.get_hooks()
    for hook in hooks:
        print "deleting hook %s on %s" % (hook.name, repo.name)
        hook.delete()

g = Github(sys.argv[1], sys.argv[2])
org = g.get_organization("coreos")
repos = org.get_repos()
for repo in repos:
    delete_all_hooks(repo)
    add_default_hooks(repo)
