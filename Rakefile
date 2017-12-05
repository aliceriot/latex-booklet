require "rake/clean"

latex_shim = "\\documentclass[12pt]{article}

\\usepackage{pdfpages}
\\includepdfset{pages=-}

\\author{N.~N}
\\title{The booklet}

\\begin{document}

    \\includepdf[pages=-,nup=1x2,landscape,signature=12]{tmp.pdf}

\\end{document}"

def strip_extension filename
  filename.gsub(/\.\w+$/, "")
end

tex_files = Rake::FileList.new("*.tex")

task default: :pdf
task pdf: tex_files.ext(".pdf")

rule ".pdf" => ".tex" do |t|
  sh "pdflatex #{t.source}"
  mv t.name, "tmp.pdf"
  sh "echo '#{latex_shim}' | pdflatex -jobname #{strip_extension t.name}"
end

CLEAN.include("*.pdf")
CLEAN.include("*.aux")
CLEAN.include("*.log")
CLEAN.include("*.toc")
