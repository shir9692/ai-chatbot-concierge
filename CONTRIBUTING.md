# Contributing to AI Chatbot Concierge

Thank you for your interest in contributing to the AI Chatbot Concierge project!

## Table of Contents
- [How to Add Collaborators](#how-to-add-collaborators)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Making Contributions](#making-contributions)

## How to Add Collaborators

If you are the repository owner or have admin access, you can add collaborators to this repository by following these steps:

### Step-by-Step Instructions:

1. **Navigate to the Repository Settings**
   - Go to the repository page: https://github.com/shir9692/ai-chatbot-concierge
   - Click on the **Settings** tab (you need admin access to see this)

2. **Access Collaborators Section**
   - In the left sidebar, click on **Collaborators and teams** (or just **Collaborators** for personal repositories)
   - You may be prompted to confirm your password for security

3. **Add a New Collaborator**
   - Click the **Add people** button
   - Enter the GitHub username, full name, or email address of the person you want to add
   - Select the correct user from the dropdown suggestions

4. **Set Permissions**
   - Choose the permission level for the collaborator:
     - **Read**: Can view and clone the repository
     - **Triage**: Can manage issues and pull requests
     - **Write**: Can push to the repository (recommended for active contributors)
     - **Maintain**: Can manage the repository without access to sensitive actions
     - **Admin**: Full access to the repository (use with caution)

5. **Send Invitation**
   - Click **Add [username] to this repository**
   - The user will receive an email invitation to collaborate
   - They must accept the invitation to gain access

### Alternative Method: Using GitHub CLI

If you prefer using the command line, you can add collaborators using the GitHub CLI:

```bash
# Install GitHub CLI if not already installed
# See: https://cli.github.com/

# Add a collaborator with write permission
gh api repos/shir9692/ai-chatbot-concierge/collaborators/USERNAME -X PUT -f permission=push

# Add a collaborator with admin permission
gh api repos/shir9692/ai-chatbot-concierge/collaborators/USERNAME -X PUT -f permission=admin
```

### Managing Collaborator Access

To modify or remove a collaborator's access:
1. Go to **Settings** → **Collaborators and teams**
2. Find the collaborator in the list
3. Click the dropdown next to their name to change permissions
4. Or click the **Remove** button to revoke access

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm (comes with Node.js)
- Git

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/shir9692/ai-chatbot-concierge.git
   cd ai-chatbot-concierge
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm start
   ```

The server will start on `http://localhost:3000` (or the port specified in server.js).

## Development Setup

### Project Structure

```
ai-chatbot-concierge/
├── index.html              # Main chatbot interface
├── prototype.html          # Prototype interface
├── server.js               # Express server
├── package.json            # Project dependencies
├── qna.json               # Q&A knowledge base
├── fallback_places.json   # Fallback location data
└── missing-features-and-gaps.txt  # Feature roadmap
```

### Testing Your Changes

Before submitting a pull request:
1. Test the chatbot interface by opening `http://localhost:3000` in your browser
2. Verify that your changes don't break existing functionality
3. Test any new features you've added

## Making Contributions

### Workflow

1. **Fork the repository** (if you're not a direct collaborator)
2. **Create a new branch** for your feature or bugfix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes** and commit them with clear, descriptive messages:
   ```bash
   git add .
   git commit -m "Add feature: description of your changes"
   ```
4. **Push to your branch**:
   ```bash
   git push origin feature/your-feature-name
   ```
5. **Open a Pull Request** from your branch to the main repository

### Code Style

- Use consistent indentation (2 spaces for JavaScript)
- Write clear, descriptive variable and function names
- Comment complex logic
- Keep functions focused and modular

### Pull Request Guidelines

- Provide a clear description of what your PR does
- Reference any related issues (e.g., "Fixes #123")
- Ensure your code is tested and working
- Be responsive to feedback and code review comments

## Questions or Issues?

If you have questions about contributing or run into any issues:
- Open an issue on GitHub: https://github.com/shir9692/ai-chatbot-concierge/issues
- Reach out to the repository maintainers

## License

By contributing to this project, you agree that your contributions will be licensed under the same license as the project.

---

Thank you for contributing to AI Chatbot Concierge! 🚀
