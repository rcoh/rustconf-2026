# Project Notes

## Slidev HTML

- Keep simple raw HTML in `slides.md` flush-left. Indentation can make Slidev parse and visibly render it as a Markdown code block.
- Put complex nested markup in a Vue component under `components/`; even flush-left sibling blocks can escape Slidev's raw HTML block and render as source text.
- Export the affected slide after changing raw HTML; a successful build alone does not catch this rendering failure.
