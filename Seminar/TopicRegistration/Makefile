# Makefile for converting Markdown to PDF using Pandoc
# Simple and efficient conversion

# Variables
CONTENT_DIR = content
RELEASE_DIR = release
HEADER_DIR = header

# Source files
PROPOSAL_MD = $(CONTENT_DIR)/proposal.md
METADATA = $(CONTENT_DIR)/metadata.yaml
TEMPLATE = $(HEADER_DIR)/template.tex

# Output files
PDF_OUTPUT = $(RELEASE_DIR)/report.pdf
HTML_OUTPUT = $(RELEASE_DIR)/report.html

# Pandoc options for PDF with custom template
PANDOC_PDF_OPTIONS = --from markdown \
                     --to pdf \
                     --pdf-engine=pdflatex \
                     --template=$(TEMPLATE) \
                     --number-sections \
                     --toc \
                     --toc-depth=3 \
                     --highlight-style=pygments \
                     --variable geometry:margin=2.5cm \
                     --variable fontsize=12pt \
                     --variable papersize=a4 \
                     --metadata-file=$(METADATA)

# Pandoc options for HTML
PANDOC_HTML_OPTIONS = --from markdown \
                      --to html5 \
                      --standalone \
                      --toc \
                      --toc-depth=3 \
                      --css=github.css \
                      --highlight-style=pygments \
                      --metadata-file=$(METADATA)

# Default target
.PHONY: all
all: clean pdf

# Convert markdown to PDF
.PHONY: pdf
pdf: $(PDF_OUTPUT)

$(PDF_OUTPUT): $(PROPOSAL_MD) $(METADATA) $(TEMPLATE) | $(RELEASE_DIR)
	@echo "Converting Markdown to PDF using custom template..."
	@pandoc $(PANDOC_PDF_OPTIONS) --output $@ $(PROPOSAL_MD)
	@echo "PDF created successfully: $@"

# Convert markdown to HTML
.PHONY: html
html: $(HTML_OUTPUT)

$(HTML_OUTPUT): $(PROPOSAL_MD) $(METADATA) | $(RELEASE_DIR)
	@echo "Converting Markdown to HTML using pandoc..."
	@pandoc $(PANDOC_HTML_OPTIONS) --output $@ $(PROPOSAL_MD)
	@echo "HTML created successfully: $@"

# Create release directory
$(RELEASE_DIR):
	@mkdir -p $(RELEASE_DIR)

# Check if pandoc is installed
.PHONY: check-pandoc
check-pandoc:
	@command -v pandoc >/dev/null 2>&1 || { \
		echo >&2 "Pandoc is not installed. Please install it first:"; \
		echo >&2 "  macOS: brew install pandoc"; \
		echo >&2 "  Ubuntu: sudo apt-get install pandoc"; \
		echo >&2 "  Windows: Download from https://pandoc.org/installing.html"; \
		exit 1; \
	}
	@echo "Pandoc is installed: $$(pandoc --version | head -n1)"

# Check if pdflatex is available
.PHONY: check-latex
check-latex:
	@command -v pdflatex >/dev/null 2>&1 || { \
		echo >&2 "pdflatex is not installed. Please install TeX Live:"; \
		echo >&2 "  macOS: brew install --cask mactex"; \
		echo >&2 "  Ubuntu: sudo apt-get install texlive-full"; \
		exit 1; \
	}
	@echo "pdflatex is available: $$(pdflatex --version | head -n1)"

# Install pandoc (macOS only)
.PHONY: install-pandoc
install-pandoc:
	@echo "Installing pandoc..."
	@brew install pandoc
	@echo "Pandoc installed successfully"

# Clean generated files
.PHONY: clean
clean:
	@echo "Cleaning generated files..."
	@rm -f $(RELEASE_DIR)/*.pdf
	@rm -f $(RELEASE_DIR)/*.html
	@echo "Clean completed"

# Help
.PHONY: help
help:
	@echo "Available targets:"
	@echo "  all           - Clean and build PDF (clean + pdf)"
	@echo "  pdf           - Convert Markdown to PDF using pandoc"
	@echo "  html          - Convert Markdown to HTML using pandoc"
	@echo "  clean         - Remove generated files"
	@echo "  check-pandoc  - Check if pandoc is installed"
	@echo "  check-latex   - Check if pdflatex is installed"
	@echo "  install-pandoc- Install pandoc (macOS only)"
	@echo "  help          - Show this help"
	@echo ""
	@echo "Quick start:"
	@echo "  make all         # Clean and build PDF"
	@echo "  make pdf         # Just build PDF"

# Debug target
.PHONY: debug
debug:
	@echo "PROPOSAL_MD: $(PROPOSAL_MD)"
	@echo "METADATA: $(METADATA)"
	@echo "PDF_OUTPUT: $(PDF_OUTPUT)"
	@echo "PANDOC_PDF_OPTIONS: $(PANDOC_PDF_OPTIONS)"
