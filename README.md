# Project Objective

The objective of this project is to build a web application utilizing the ChatGPT API with a focus on creating a nostalgic, retro-inspired user interface (UI). The design captures the essence of 90s computing with terminal-style animations and sound effects.

`Instagram Reel Reference`: [Retro UI Design](https://www.instagram.com/reel/DAJsgVSgGsX/?igsh=MnMwM2k0MzFqZTYy)

`Note: Figma files are yet to be updated`

# How to Contribute

## For Internal Contributors (GitHub Flow - Feature Branch Workflow)

1. **Clone the Repository**: Clone the repository to your local machine.
   ```bash
   git clone https://github.com/djx-community/retro-gpt.git
   ```
   
2. **Create a New Branch**: Work on a new branch specific to your feature or fix.
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make Your Changes**: Implement your feature or bug fix.

4. **Push the Changes**: Once your changes are ready, push the branch to the repository.
   ```bash
   git push origin feature/your-feature-name
   ```

5. **Open a Pull Request (PR)**: Submit a PR from your feature branch to the `master` branch, clearly describing the changes.

6. **Code Review**: Wait for the code to be reviewed, address any comments, and merge the PR after approval.

---

## For Outside Collaborators (Open Source Contribution)

1. **Fork the Repository**: Fork this repository to your GitHub account.
   
2. **Clone the Forked Repository**: Clone the forked repository to your local machine.
   ```bash
   git clone https://github.com/your-username/retro-gpt.git
   ```

3. **Create a New Branch**: Create a new branch in your fork to work on your feature or fix.
   ```bash
   git checkout -b feature/your-feature-name
   ```

4. **Make Your Changes**: Implement your feature or bug fix.

5. **Commit and Push**: Once your changes are complete, commit and push them to your fork.
   ```bash
   git add .
   git commit -m "Description of changes"
   git push origin feature/your-feature-name
   ```

6. **Submit a Pull Request**: Open a pull request (PR) from your forked repository to this repository’s `main` branch, detailing your changes.

Here's the updated **Developing** section for your README file:

---

## Developing

The development tasks for this project are organized into issues on the GitHub repository. Each issue may contain a checklist of subtasks that can be turned into separate issues if needed.

### Steps to Start Developing

1. **View Project Issues**: Go to the [Issues](https://github.com/djx-community/retro-gpt/issues) tab on GitHub to see the list of tasks. Only commit to issues that are currently **unassigned**.
   
2. **Assign Issues (Internal Collaborators)**: 
   - Internal collaborators can assign themselves to an issue before starting work by clicking the "Assignees" section within the issue.
   
3. **Fork and Clone (Outside Collaborators)**: 
   - For external contributors, fork the repository and then clone it to your local machine. 
   ```bash
   git clone https://github.com/your-username/retro-gpt.git
   ```

4. **Create a Feature Branch**: After assigning or selecting an issue to work on, create a new branch to work on your feature or fix.
   ```bash
   git checkout -b feature/your-feature-name
   ```

5. **Make Your Changes**: Implement the assigned task by addressing the issue or its subtasks. 

6. **Push and Submit a PR**: Once you've completed the task, push your branch and submit a pull request (PR) referencing the issue number in the PR description. Internal collaborators can directly submit a PR after assigning themselves.

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.
