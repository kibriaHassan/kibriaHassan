name: Generate Snake

on:
  schedule:
    - cron: "0 */12 * * *"  # প্রতি 12 ঘন্টায় auto update হবে
  workflow_dispatch:  # ম্যানুয়ালি চালানোর জন্য

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Generate Snake Graph
        uses: Platane/snk@v3
        with:
          github_user_name: kibriaHassan
          outputs: dist/snake.svg

      - name: Push Snake to output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
