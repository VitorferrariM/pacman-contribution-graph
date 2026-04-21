name: Generate Pacman Contribution Graph

on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:

jobs:
  generate:
    runs-on: ubuntu-latest

    steps:
      - name: generate pacman graph
        uses: Platane/snk@v3
        with:
          github_user_name: VitorferrariM
          outputs: |
            output/pacman-contribution-graph.svg
            output/pacman-contribution-graph-dark.svg?palette=github-dark

      - name: push pacman graph
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: output
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
