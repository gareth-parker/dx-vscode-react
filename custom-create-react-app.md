# Forking CRA for a custom configuration

1.  Fork the main repo: [Create React App](https://github.com/facebook/create-react-app)

2.  `git clone https://github.com/<user>/create-react-app`

3.  `cd create-react-app`

4.  `git checkout master`

5.  Check remotes:
    `git remote -v`

6.  Create an upstream to source so you can rebase new updates into your forked repo
    `git remote add upstream https://github.com/facebook/create-react-app`

7.  Create a branch for the customisations:
    `git checkout -b custom-react-scripts`

8.  Make changes and install any new dependencies...

To pull in updates from the main repo:
`git fetch upstream` -> `git rebase upstream/master`
