<h1>oi, me chamo André Luis</h1>
<p>Estou atualmente cursando Analise e Desenvolvimento de Sistemas e Aprendendo o Protheus ADVPL</p>
<h2>🚀Algumas linguagens e ferramentas que já utilizei</h2>
<p><a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" alt="java" width="42" height="42" /></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="42" height="42" /></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="html5" width="42" height="42" /></a>
<a target="_blank" href="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" style="display: inline-block;"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" alt="css3" width="42" height="42" /></a>
<a target="_blank" href="https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg" style="display: inline-block;"><img src="https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg" alt="mssql" width="42" height="42" /></a>
<a target="_blank" href="https://www.vectorlogo.zone/logos/unity3d/unity3d-icon.svg" style="display: inline-block;"><img src="https://www.vectorlogo.zone/logos/unity3d/unity3d-icon.svg" alt="unity" width="42" height="42" /></a>
<a target="_blank" href="https://cdn.worldvectorlogo.com/logos/arduino-1.svg" style="display: inline-block;"><img src="https://cdn.worldvectorlogo.com/logos/arduino-1.svg" alt="arduino" width="42" height="42" /></a></p>
<h2>✒️ Recent Posts</h2>
<ul>
<li><a target="_blank" href=""></a></li>
<h2>⚡️onde me encontrar</h2>
<p><a target="_blank" href="https://twitter.com/andrebao_" style="display: inline-block;"><img src="https://img.shields.io/badge/twitter-x?style=for-the-badge&logo=x&logoColor=white&color=%230f1419" alt="twitter" /></a></p>

name: GitHub Snake Game

on:
  # Schedule the workflow to run daily at midnight UTC
  schedule:
    - cron: "0 0 * * *"
  # Allow manual triggering of the workflow
  workflow_dispatch:
  # Trigger the workflow on pushes to the main branch
  push:
    branches:
      - main
jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      # Step 1: Checkout the repository
      - name: Checkout Repository
        uses: actions/checkout@v3
      # Step 2: Generate the snake animations
      - name: Generate GitHub Contributions Snake Animations
        uses: Platane/snk@v3
        with:
          # GitHub username to generate the animation for
          github_user_name: ${{ github.repository_owner }}
          # Define the output files and their configurations
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
            dist/ocean.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      # Step 3: Deploy the generated files to the 'output' branch
      - name: Deploy to Output Branch
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: output
          # Optionally, you can set a custom commit message
          commit_message: "Update snake animation [skip ci]"
