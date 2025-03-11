.PHONY: live live-all build build-all clean

live:
	@echo "Previewing system design slides..."
	-@reveal-md sys.md -w --scripts https://cdn.tonycrane.cc/heti/heti.js,heti_worker.js --template template.html || true

live-%:
	@echo "Previewing $* slides..."
	-@reveal-md $*.md -w --scripts https://cdn.tonycrane.cc/heti/heti.js,heti_worker.js --template template.html || true

live-all:
	@echo "Choose a specific slide to preview:"
	@echo "  make live     - Preview system design slides"
	@for slide in $$(ls *.md | grep -v sys.md | sed 's/\.md//g'); do \
		echo "  make live-$$slide - Preview $$slide slides"; \
	done

build:
	@echo "Building slides to ../site..."
	@mkdir -p ../site
	
	@echo "Building all slides..."
	@ALL_SLIDES=""
	@for slide in $$(ls *.md); do \
		echo "Building $$slide slides..."; \
		filename=$$(basename "$$slide" .md); \
		title=$$(head -n 1 "$$slide" | sed 's/^#\s*//'); \
		mkdir -p "../site/$$filename"; \
		reveal-md "$$slide" --scripts https://cdn.tonycrane.cc/heti/heti.js,heti_worker.js --template template.html --static "../site/$$filename" --assets-dir "assets"; \
		mv "../site/$$filename/$$filename.html" "../site/$$filename/index.html"; \
		SLIDE_CLASS=""; \
		if [ "$$filename" = "sys" ]; then \
			SLIDE_CLASS="class=\\\"main-slide\\\""; \
		fi; \
		ALL_SLIDES="$$ALL_SLIDES\n    <li $$SLIDE_CLASS><a href=\\\"./$$filename/\\\">$$title</a></li>"; \
	done
	
	@cp -r sys3 ../site/
	@cp custom.css ../site/
	@cp heti_worker.js ../site/
	
	@echo "Generating index page..."
	@if [ -f "index.html" ]; then \
		cp index.html ../site/index.html.template; \
		sed "s|<li class=\"main-slide\"><a href=\"./sys/\">系统设计幻灯片</a></li>\\s*<li><a href=\"./example/\">示例幻灯片</a></li>\\s*<li><a href=\"./home/\">幻灯片导航</a></li>|$$ALL_SLIDES|g" ../site/index.html.template > ../site/index.html; \
		rm ../site/index.html.template; \
	else \
		echo "<!DOCTYPE html>" > ../site/index.html; \
		echo "<html lang=\"zh-CN\">" >> ../site/index.html; \
		echo "<head>" >> ../site/index.html; \
		echo "  <meta charset=\"UTF-8\">" >> ../site/index.html; \
		echo "  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">" >> ../site/index.html; \
		echo "  <title>幻灯片集合</title>" >> ../site/index.html; \
		echo "  <link rel=\"stylesheet\" href=\"custom.css\">" >> ../site/index.html; \
		echo "  <style>" >> ../site/index.html; \
		echo "    body{font-family:system-ui,-apple-system,BlinkMacSystemFont,sans-serif;max-width:900px;margin:0 auto;padding:40px 20px;line-height:1.6}" >> ../site/index.html; \
		echo "    .header{text-align:center;margin-bottom:40px}" >> ../site/index.html; \
		echo "    .header h1{font-size:2.5em;margin-bottom:10px}" >> ../site/index.html; \
		echo "    .header p{font-size:1.2em;color:#666}" >> ../site/index.html; \
		echo "    .slides-list{list-style:none;padding:0;display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:20px}" >> ../site/index.html; \
		echo "    .slides-list li{border-radius:8px;background:#f5f5f5;transition:all 0.3s ease;box-shadow:0 2px 5px rgba(0,0,0,0.1)}" >> ../site/index.html; \
		echo "    .slides-list li:hover{transform:translateY(-5px);box-shadow:0 5px 15px rgba(0,0,0,0.1)}" >> ../site/index.html; \
		echo "    .slides-list a{display:block;padding:25px;font-size:1.2em;color:#333;text-decoration:none}" >> ../site/index.html; \
		echo "    .slides-list a:hover{color:#0066cc}" >> ../site/index.html; \
		echo "    .main-slide{background:#e6f7ff!important;border-left:4px solid #0066cc}" >> ../site/index.html; \
		echo "    .description{margin:40px 0;padding:20px;background:#f9f9f9;border-radius:8px}" >> ../site/index.html; \
		echo "    .footer{margin-top:40px;text-align:center;font-size:0.9em;color:#666}" >> ../site/index.html; \
		echo "  </style>" >> ../site/index.html; \
		echo "</head>" >> ../site/index.html; \
		echo "<body>" >> ../site/index.html; \
		echo "  <div class=\"header\">" >> ../site/index.html; \
		echo "    <h1>幻灯片集合</h1>" >> ../site/index.html; \
		echo "    <p>系统设计及各种主题的幻灯片</p>" >> ../site/index.html; \
		echo "  </div>" >> ../site/index.html; \
		echo "  <div class=\"description\">" >> ../site/index.html; \
		echo "    <h2>关于本站</h2>" >> ../site/index.html; \
		echo "    <p>本站托管了多个幻灯片，每个幻灯片都有独立的URL路径。您可以通过下面的链接访问各个幻灯片。</p>" >> ../site/index.html; \
		echo "    <p>所有幻灯片均使用reveal.js制作，支持全屏浏览和演示者模式。在幻灯片页面按<kbd>F</kbd>键进入全屏，按<kbd>ESC</kbd>退出。</p>" >> ../site/index.html; \
		echo "  </div>" >> ../site/index.html; \
		echo "  <h2>可用幻灯片</h2>" >> ../site/index.html; \
		echo "  <ul class=\"slides-list\">$$ALL_SLIDES" >> ../site/index.html; \
		echo "  </ul>" >> ../site/index.html; \
		echo "  <div class=\"footer\">" >> ../site/index.html; \
		echo "    <p>使用 reveal-md 和 GitHub Pages 构建</p>" >> ../site/index.html; \
		echo "  </div>" >> ../site/index.html; \
		echo "</body>" >> ../site/index.html; \
		echo "</html>" >> ../site/index.html; \
	fi
	
	@echo "Creating slides index..."
	@echo "<!DOCTYPE html>" > ../site/slides.html
	@echo "<html><head><meta charset=\"UTF-8\"><meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">" >> ../site/slides.html
	@echo "<title>幻灯片索引</title><link rel=\"stylesheet\" href=\"custom.css\"><style>" >> ../site/slides.html
	@echo "body{font-family:system-ui,-apple-system,BlinkMacSystemFont,sans-serif;max-width:800px;margin:0 auto;padding:20px}" >> ../site/slides.html
	@echo ".slides-list{list-style:none;padding:0}.slides-list li{margin:15px 0;padding:15px;border-radius:8px;background:#f5f5f5}" >> ../site/slides.html
	@echo ".slides-list a{display:block;font-size:1.2em;color:#333;text-decoration:none}.slides-list a:hover{color:#0066cc}" >> ../site/slides.html
	@echo "h1{margin-bottom:30px}</style></head><body><h1>幻灯片索引</h1><ul class=\"slides-list\">" >> ../site/slides.html
	@echo "<li><a href=\"./\">首页</a></li>$$ALL_SLIDES" >> ../site/slides.html
	@echo "</ul></body></html>" >> ../site/slides.html
	
	@echo "Build complete!"

build-all: build

clean:
	@echo "Cleaning up..."
	rm -rf ../site/
