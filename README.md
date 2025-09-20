name: Generate Snake

on:
  schedule: # Runs every 12 hours
    - cron: "0 */12 * * *"
  workflow_dispatch: # Allow manual trigger

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Generate Snake Game from Contributions
        uses: Platane/snk@v3
        with:
          github_user_name: Vishnu-Varthan1
          outputs: dist/snake.svg dist/snake-dark.svg

      - name: Push Snake to GitHub Pages
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
