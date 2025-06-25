this is a fully customizable shopify theme code 

<!-- theme.liquid - Main theme layout file -->
<!DOCTYPE html>
<html lang="{{ shop.locale }}">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>{{ page_title }}{% if current_tags %} &ndash; {{ 'general.meta.tags' | t: tags: current_tags | join: ', ' }}{% endif %}{% if current_page != 1 %} &ndash; {{ 'general.meta.page' | t: page: current_page }}{% endif %}{% unless page_title contains shop.name %} &ndash; {{ shop.name }}{% endunless %}</title>
  
  {% if page_description %}
    <meta name="description" content="{{ page_description | escape }}">
  {% endif %}
  
  <!-- Favicon -->
  {% if settings.favicon != blank %}
    <link rel="shortcut icon" href="{{ settings.favicon | img_url: '32x32' }}" type="image/png">
  {% endif %}
  
  <!-- Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family={{ settings.heading_font.family | replace: ' ', '+' }}:ital,wght@0,400;0,500;0,600;0,700;0,800;0,900;1,400;1,500;1,600;1,700;1,800;1,900&family={{ settings.body_font.family | replace: ' ', '+' }}:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,500;1,600;1,700&family={{ settings.accent_font.family | replace: ' ', '+' }}:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
  
  <!-- Stylesheets -->
  {{ 'theme.css' | asset_url | stylesheet_tag }}
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  
  <!-- Theme settings CSS variables -->
  <style>
    :root {
      /* Colors */
      --primary-color: {{ settings.primary_color }};
      --primary-color-rgb: {{ settings.primary_color | color_to_rgb | split: ',' | join: ', ' }};
      --secondary-color: {{ settings.secondary_color }};
      --secondary-color-rgb: {{ settings.secondary_color | color_to_rgb | split: ',' | join: ', ' }};
      --accent-color: {{ settings.accent_color }};
      --accent-color-rgb: {{ settings.accent_color | color_to_rgb | split: ',' | join: ', ' }};
      --background-color: {{ settings.background_color }};
      --background-color-rgb: {{ settings.background_color | color_to_rgb | split: ',' | join: ', ' }};
      --text-color: {{ settings.text_color }};
      --text-color-rgb: {{ settings.text_color | color_to_rgb | split: ',' | join: ', ' }};
      --light-text-color: {{ settings.light_text_color }};
      --border-color: {{ settings.border_color }};
      --success-color: {{ settings.success_color }};
      --error-color: {{ settings.error_color }};
      --warning-color: {{ settings.warning_color }};
      --info-color: {{ settings.info_color }};
      
      /* Typography */
      --heading-font: {{ settings.heading_font.family }}, {{ settings.heading_font.fallback_families }};
      --body-font: {{ settings.body_font.family }}, {{ settings.body_font.fallback_families }};
      --accent-font: {{ settings.accent_font.family }}, {{ settings.accent_font.fallback_families }};
      --base-font-size: {{ settings.base_font_size }}px;
      --heading-scale-ratio: {{ settings.heading_scale_ratio }};
      --heading-line-height: {{ settings.heading_line_height }};
      --body-line-height: {{ settings.body_line_height }};
      --letter-spacing: {{ settings.letter_spacing }}em;
      
      /* Spacing */
      --section-spacing: {{ settings.section_spacing }}px;
      --container-padding: {{ settings.container_padding }}px;
      --element-spacing: {{ settings.element_spacing }}px;
      --grid-gap: {{ settings.grid_gap }}px;
      
      /* Border Radius */
      --border-radius-small: {{ settings.border_radius_small }}px;
      --border-radius: {{ settings.border_radius }}px;
      --border-radius-large: {{ settings.border_radius_large }}px;
      
      /* Animation */
      --animation-speed: {{ settings.animation_speed }}s;
      --transition-timing: {{ settings.transition_timing }};
      
      /* Shadows */
      --box-shadow: {{ settings.box_shadow }};
      --text-shadow: {{ settings.text_shadow }};
      
      /* Layout */
      --container-width: {{ settings.container_width }}px;
      --header-height: {{ settings.header_height }}px;
      --footer-padding: {{ settings.footer_padding }}px;
      
      /* Button Styles */
      --button-padding-y: {{ settings.button_padding_y }}px;
      --button-padding-x: {{ settings.button_padding_x }}px;
    }
    
    /* Base Styles */
    html {
      font-size: var(--base-font-size);
    }
    
    body {
      background-color: var(--background-color);
      color: var(--text-color);
      font-family: var(--body-font);
      font-size: 1rem;
      line-height: var(--body-line-height);
      letter-spacing: var(--letter-spacing);
      margin: 0;
      padding: 0;
    }
    
    h1, h2, h3, h4, h5, h6 {
      font-family: var(--heading-font);
      line-height: var(--heading-line-height);
      margin-top: 0;
      font-weight: {{ settings.heading_weight }};
    }
    
    h1 { font-size: calc(1rem * var(--heading-scale-ratio) * var(--heading-scale-ratio) * var(--heading-scale-ratio) * var(--heading-scale-ratio)); }
    h2 { font-size: calc(1rem * var(--heading-scale-ratio) * var(--heading-scale-ratio) * var(--heading-scale-ratio)); }
    h3 { font-size: calc(1rem * var(--heading-scale-ratio) * var(--heading-scale-ratio)); }
    h4 { font-size: calc(1rem * var(--heading-scale-ratio)); }
    h5 { font-size: 1rem; }
    h6 { font-size: calc(1rem / var(--heading-scale-ratio)); }
    
    a {
      color: var(--primary-color);
      text-decoration: {{ settings.link_style }};
      transition: all var(--animation-speed) var(--transition-timing);
    }
    
    a:hover {
      color: var(--secondary-color);
    }
    
    img {
      max-width: 100%;
      height: auto;
    }
    
    .container {
      max-width: var(--container-width);
      margin-left: auto;
      margin-right: auto;
      padding-left: var(--container-padding);
      padding-right: var(--container-padding);
    }
    
    /* Theme Styles */
    {% if settings.theme_style == 'modern' %}
      /* Modern Theme Styles */
      .theme-button {
        background-color: var(--primary-color);
        color: white;
        border: none;
        border-radius: var(--border-radius);
        padding: var(--button-padding-y) var(--button-padding-x);
        font-family: var(--accent-font);
        font-weight: 600;
        transition: all var(--animation-speed) var(--transition-timing);
      }
      
      .theme-button:hover {
        background-color: var(--secondary-color);
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      }
      
      .card {
        background-color: white;
        border-radius: var(--border-radius);
        box-shadow: var(--box-shadow);
        overflow: hidden;
      }
      
    {% elsif settings.theme_style == 'minimal' %}
      /* Minimal Theme Styles */
      .theme-button {
        background-color: transparent;
        color: var(--primary-color);
        border: 1px solid var(--primary-color);
        border-radius: var(--border-radius);
        padding: var(--button-padding-y) var(--button-padding-x);
        font-family: var(--accent-font);
        font-weight: 500;
        transition: all var(--animation-speed) var(--transition-timing);
      }
      
      .theme-button:hover {
        background-color: var(--primary-color);
        color: white;
      }
      
      .card {
        background-color: white;
        border: 1px solid var(--border-color);
        border-radius: var(--border-radius);
      }
      
    {% elsif settings.theme_style == 'bold' %}
      /* Bold Theme Styles */
      .theme-button {
        background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
        color: white;
        border: none;
        border-radius: var(--border-radius-large);
        padding: var(--button-padding-y) var(--button-padding-x);
        font-family: var(--accent-font);
        font-weight: 700;
        text-transform: uppercase;
        letter-spacing: 0.1em;
        transition: all var(--animation-speed) var(--transition-timing);
      }
      
      .theme-button:hover {
        transform: scale(1.05);
        box-shadow: 0 5px 15px rgba(var(--primary-color-rgb), 0.4);
      }
      
      .card {
        background-color: white;
        border-radius: var(--border-radius);
        box-shadow: var(--box-shadow);
        border-left: 4px solid var(--primary-color);
      }
      
    {% elsif settings.theme_style == 'classic' %}
      /* Classic Theme Styles */
      .theme-button {
        background-color: var(--primary-color);
        color: white;
        border: none;
        border-radius: var(--border-radius-small);
        padding: var(--button-padding-y) var(--button-padding-x);
        font-family: var(--accent-font);
        font-weight: 600;
        transition: all var(--animation-speed) var(--transition-timing);
      }
      
      .theme-button:hover {
        background-color: var(--secondary-color);
      }
      
      .card {
        background-color: white;
        border: 1px solid var(--border-color);
        border-radius: var(--border-radius-small);
      }
      
    {% elsif settings.theme_style == 'y2k' %}
      /* Y2K Theme Styles */
      .chrome-text {
        background: linear-gradient(to right, #f0f0f0, #c0c0c0, #ffffff, #c0c0c0);
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        text-shadow: 0 0 10px rgba(var(--primary-color-rgb), 0.5);
      }
      
      .y2k-text {
        background: linear-gradient(to right, var(--primary-color), var(--secondary-color), var(--accent-color));
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        text-shadow: 0 0 10px rgba(var(--primary-color-rgb), 0.5);
      }
      
      .chrome-heart {
        background: linear-gradient(135deg, #ffffff, #c0c0c0, #ffffff, #c0c0c0);
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        filter: drop-shadow(0 0 5px rgba(var(--primary-color-rgb), 0.7));
      }
      
      .glow-star {
        color: white;
        text-shadow: 0 0 10px #ffffff, 0 0 20px #ffffff;
        opacity: 0.9;
      }
      
      .y2k-border {
        border: 3px solid transparent;
        background: linear-gradient(var(--background-color), var(--background-color)) padding-box,
                    linear-gradient(to right, var(--primary-color), var(--secondary-color), var(--accent-color)) border-box;
        border-radius: var(--border-radius);
      }
      
      .y2k-bubble {
        position: absolute;
        border-radius: 50%;
        background: linear-gradient(135deg, rgba(var(--primary-color-rgb), 0.2), rgba(var(--secondary-color-rgb), 0.2));
        box-shadow: inset 0 0 20px rgba(255,255,255,0.2);
        animation: bubbleFloat var(--animation-speed) ease-in-out infinite;
      }
      
      @keyframes bubbleFloat {
        0% { transform: translateY(0) rotate(0deg); }
        50% { transform: translateY(-20px) rotate(5deg); }
        100% { transform: translateY(0) rotate(0deg); }
      }
      
      .y2k-grid {
        background-image: linear-gradient(rgba(var(--primary-color-rgb), 0.1) 1px, transparent 1px),
                          linear-gradient(90deg, rgba(var(--primary-color-rgb), 0.1) 1px, transparent 1px);
        background-size: 20px 20px;
      }
      
      .theme-button {
        position: relative;
        z-index: 1;
        overflow: hidden;
        font-family: var(--accent-font);
        letter-spacing: 1px;
        background-color: var(--primary-color);
        color: white;
        border: none;
        border-radius: 9999px;
        padding: var(--button-padding-y) var(--button-padding-x);
        cursor: pointer;
        transition: all var(--animation-speed) var(--transition-timing);
      }
      
      .theme-button:hover {
        background-color: var(--secondary-color);
      }
      
      .theme-button::before {
        content: '';
        position: absolute;
        top: -2px;
        left: -2px;
        right: -2px;
        bottom: -2px;
        z-index: -1;
        background: linear-gradient(45deg, var(--primary-color), var(--secondary-color), var(--accent-color), var(--secondary-color));
        background-size: 400%;
        border-radius: 10px;
        animation: glowing 20s linear infinite;
        opacity: 0;
        transition: opacity var(--animation-speed) ease-in-out;
      }
      
      .theme-button:hover::before {
        opacity: 1;
      }
      
      @keyframes glowing {
        0% { background-position: 0 0; }
        50% { background-position: 400% 0; }
        100% { background-position: 0 0; }
      }
      
      .card {
        background-color: rgba(255, 255, 255, 0.1);
        backdrop-filter: blur(10px);
        border-radius: var(--border-radius);
        border: 3px solid transparent;
        background-clip: padding-box;
        background-image: linear-gradient(var(--background-color), var(--background-color)) padding-box,
                          linear-gradient(to right, var(--primary-color), var(--secondary-color)) border-box;
      }
    {% endif %}
    
    /* Custom styles based on theme settings */
    {% if settings.enable_animations == false %}
    .y2k-bubble, .theme-button::before {
      animation: none !important;
    }
    {% endif %}
    
    /* Additional custom CSS from theme settings */
    {{ settings.custom_css }}
  </style>
  
  <!-- Shopify required -->
  {{ content_for_header }}
</head>
<body class="template-{{ template | split: '.' | first }} theme-{{ settings.theme_style }}">
  <!-- Background Effects -->
  {% if settings.enable_background_effects %}
    <div class="background-effects" id="backgroundEffects"></div>
  {% endif %}
  
  <!-- Announcement Bar -->
  {% if settings.show_announcement %}
    {% section 'announcement-bar' %}
  {% endif %}
  
  <!-- Header -->
  {% section 'header' %}
  
  <!-- Main Content -->
  <main role="main" id="MainContent">
    {{ content_for_layout }}
  </main>
  
  <!-- Footer -->
  {% section 'footer' %}
  
  <!-- Scripts -->
  {{ 'theme.js' | asset_url | script_tag }}
  
  <script>
    // Create background effects based on theme style
    function createBackgroundEffects() {
      const backgroundEffects = document.getElementById('backgroundEffects');
      if (!backgroundEffects) return;
      
      {% if settings.theme_style == 'y2k' %}
        // Create stars
        const numberOfStars = {{ settings.background_density }};
        
        for (let i = 0; i < numberOfStars; i++) {
          const star = document.createElement('div');
          star.classList.add('star');
          star.innerHTML = i % 3 === 0 ? '★' : '✧';
          star.classList.add('glow-star');
          star.style.left = `${Math.random() * 100}%`;
          star.style.top = `${Math.random() * 100}%`;
          star.style.fontSize = `${Math.random() * 10 + 8}px`;
          star.style.animationDelay = `${Math.random() * 5}s`;
          star.style.position = 'absolute';
          star.style.opacity = '0';
          star.style.animation = 'twinkle 5s infinite';
          star.style.pointerEvents = 'none';
          star.style.zIndex = '0';
          backgroundEffects.appendChild(star);
        }
        
        // Create bubbles
        const numberOfBubbles = {{ settings.background_density }} / 2;
        
        for (let i = 0; i < numberOfBubbles; i++) {
          const bubble = document.createElement('div');
          bubble.classList.add('y2k-bubble');
          const size = Math.random() * 100 + 50;
          bubble.style.width = `${size}px`;
          bubble.style.height = `${size}px`;
          bubble.style.left = `${Math.random() * 100}%`;
          bubble.style.top = `${Math.random() * 100}%`;
          bubble.style.animationDelay = `${Math.random() * 5}s`;
          bubble.style.animationDuration = `${Math.random() * 10 + 10}s`;
          backgroundEffects.appendChild(bubble);
        }
      {% elsif settings.theme_style == 'modern' %}
        // Create modern background elements
        const numberOfElements = {{ settings.background_density }};
        
        for (let i = 0; i < numberOfElements; i++) {
          const element = document.createElement('div');
          element.style.position = 'absolute';
          element.style.width = `${Math.random() * 200 + 50}px`;
          element.style.height = `${Math.random() * 200 + 50}px`;
          element.style.borderRadius = '50%';
          element.style.background = `radial-gradient(circle, rgba(var(--primary-color-rgb), 0.05), rgba(var(--secondary-color-rgb), 0.02))`;
          element.style.left = `${Math.random() * 100}%`;
          element.style.top = `${Math.random() * 100}%`;
          element.style.pointerEvents = 'none';
          element.style.zIndex = '0';
          backgroundEffects.appendChild(element);
        }
      {% endif %}
    }
    
    // Initialize
    document.addEventListener('DOMContentLoaded', () => {
      {% if settings.enable_background_effects %}
      createBackgroundEffects();
      {% endif %}
      
      // Initialize other scripts
      initializeAccordions();
      initializeSliders();
      initializeMobileMenu();
      initializeModals();
      initializeDropdowns();
      initializeTooltips();
      initializeQuantitySelectors();
      initializeProductOptions();
      
      // Initialize theme-specific features
      {% if settings.enable_quick_view %}
      initializeQuickView();
      {% endif %}
      
      {% if settings.enable_sticky_add_to_cart %}
      initializeStickyAddToCart();
      {% endif %}
      
      {% if settings.enable_ajax_cart %}
      initializeAjaxCart();
      {% endif %}
    });
    
    // Accordion functionality
    function initializeAccordions() {
      const accordionButtons = document.querySelectorAll('.accordion-trigger');
      
      accordionButtons.forEach(button => {
        button.addEventListener('click', () => {
          const targetId = button.getAttribute('data-target');
          const content = document.getElementById(targetId);
          const icon = button.querySelector('.accordion-icon');
          
          // Toggle the current content
          content.classList.toggle('hidden');
          if (icon) {
            icon.classList.toggle('rotate-180');
          }
          
          // Close other accordions in the same group
          const groupId = button.getAttribute('data-group');
          if (groupId) {
            const groupButtons = document.querySelectorAll(`.accordion-trigger[data-group="${groupId}"]`);
            groupButtons.forEach(otherButton => {
              if (otherButton !== button) {
                const otherId = otherButton.getAttribute('data-target');
                const otherContent = document.getElementById(otherId);
                const otherIcon = otherButton.querySelector('.accordion-icon');
                
                if (otherContent && !otherContent.classList.contains('hidden')) {
                  otherContent.classList.add('hidden');
                  if (otherIcon) {
                    otherIcon.classList.remove('rotate-180');
                  }
                }
              }
            });
          }
        });
      });
    }
    
    // Mobile menu functionality
    function initializeMobileMenu() {
      const mobileMenuButton = document.getElementById('mobileMenuButton');
      const mobileMenu = document.getElementById('mobileMenu');
      
      if (mobileMenuButton && mobileMenu) {
        mobileMenuButton.addEventListener('click', () => {
          mobileMenu.classList.toggle('hidden');
          document.body.classList.toggle('mobile-menu-open');
        });
      }
    }
    
    // Slider functionality
    function initializeSliders() {
      const sliders = document.querySelectorAll('.slider-container');
      
      sliders.forEach(slider => {
        const slidesContainer = slider.querySelector('.slides');
        const prevButton = slider.querySelector('.prev-slide');
        const nextButton = slider.querySelector('.next-slide');
        const dots = slider.querySelectorAll('.slider-dot');
        
        if (!slidesContainer) return;
        
        let currentSlide = 0;
        const slideCount = slidesContainer.children.length;
        
        function updateSlider() {
          slidesContainer.style.transform = `translateX(-${currentSlide * 100}%)`;
          
          // Update dots
          dots.forEach((dot, index) => {
            dot.classList.toggle('active', index === currentSlide);
          });
        }
        
        if (prevButton) {
          prevButton.addEventListener('click', () => {
            currentSlide = (currentSlide - 1 + slideCount) % slideCount;
            updateSlider();
          });
        }
        
        if (nextButton) {
          nextButton.addEventListener('click', () => {
            currentSlide = (currentSlide + 1) % slideCount;
            updateSlider();
          });
        }
        
        // Add dot click handlers
        dots.forEach((dot, index) => {
          dot.addEventListener('click', () => {
            currentSlide = index;
            updateSlider();
          });
        });
        
        // Auto-advance if enabled
        const autoAdvance = slider.getAttribute('data-auto-advance') === 'true';
        const interval = parseInt(slider.getAttribute('data-interval') || '5000');
        
        if (autoAdvance && slideCount > 1) {
          setInterval(() => {
            currentSlide = (currentSlide + 1) % slideCount;
            updateSlider();
          }, interval);
        }
        
        // Touch/swipe support
        let touchStartX = 0;
        let touchEndX = 0;
        
        slidesContainer.addEventListener('touchstart', (e) => {
          touchStartX = e.changedTouches[0].screenX;
        });
        
        slidesContainer.addEventListener('touchend', (e) => {
          touchEndX = e.changedTouches[0].screenX;
          handleSwipe();
        });
        
        function handleSwipe() {
          const swipeThreshold = 50;
          if (touchEndX < touchStartX - swipeThreshold) {
            // Swipe left
            currentSlide = (currentSlide + 1) % slideCount;
            updateSlider();
          } else if (touchEndX > touchStartX + swipeThreshold) {
            // Swipe right
            currentSlide = (currentSlide - 1 + slideCount) % slideCount;
            updateSlider();
          }
        }
      });
    }
    
    // Modal functionality
    function initializeModals() {
      const modalTriggers = document.querySelectorAll('[data-modal-target]');
      const modalCloseButtons = document.querySelectorAll('[data-modal-close]');
      
      modalTriggers.forEach(trigger => {
        trigger.addEventListener('click', () => {
          const targetId = trigger.getAttribute('data-modal-target');
          const modal = document.getElementById(targetId);
          
          if (modal) {
            modal.classList.remove('hidden');
            document.body.classList.add('modal-open');
            
            // Close modal when clicking outside
            modal.addEventListener('click', (e) => {
              if (e.target === modal) {
                modal.classList.add('hidden');
                document.body.classList.remove('modal-open');
              }
            });
          }
        });
      });
      
      modalCloseButtons.forEach(button => {
        button.addEventListener('click', () => {
          const modal = button.closest('.modal');
          if (modal) {
            modal.classList.add('hidden');
            document.body.classList.remove('modal-open');
          }
        });
      });
      
      // Close modal with Escape key
      document.addEventListener('keydown', (e) => {
        if (e.key === 'Escape') {
          const openModal = document.querySelector('.modal:not(.hidden)');
          if (openModal) {
            openModal.classList.add('hidden');
            document.body.classList.remove('modal-open');
          }
        }
      });
    }
    
    // Dropdown functionality
    function initializeDropdowns() {
      const dropdownTriggers = document.querySelectorAll('.dropdown-trigger');
      
      dropdownTriggers.forEach(trigger => {
        trigger.addEventListener('click', (e) => {
          e.stopPropagation();
          const dropdown = trigger.nextElementSibling;
          
          // Close all other dropdowns
          document.querySelectorAll('.dropdown-content').forEach(content => {
            if (content !== dropdown) {
              content.classList.add('hidden');
            }
          });
          
          // Toggle current dropdown
          dropdown.classList.toggle('hidden');
        });
      });
      
      // Close dropdowns when clicking outside
      document.addEventListener('click', () => {
        document.querySelectorAll('.dropdown-content').forEach(content => {
          content.classList.add('hidden');
        });
      });
    }
    
    // Tooltip functionality
    function initializeTooltips() {
      const tooltipTriggers = document.querySelectorAll('[data-tooltip]');
      
      tooltipTriggers.forEach(trigger => {
        const tooltipText = trigger.getAttribute('data-tooltip');
        const tooltipPosition = trigger.getAttribute('data-tooltip-position') || 'top';
        
        trigger.addEventListener('mouseenter', () => {
          const tooltip = document.createElement('div');
          tooltip.classList.add('tooltip', `tooltip-${tooltipPosition}`);
          tooltip.textContent = tooltipText;
          document.body.appendChild(tooltip);
          
          const triggerRect = trigger.getBoundingClientRect();
          const tooltipRect = tooltip.getBoundingClientRect();
          
          let top, left;
          
          switch (tooltipPosition) {
            case 'top':
              top = triggerRect.top - tooltipRect.height - 10;
              left = triggerRect.left + (triggerRect.width / 2) - (tooltipRect.width / 2);
              break;
            case 'bottom':
              top = triggerRect.bottom + 10;
              left = triggerRect.left + (triggerRect.width / 2) - (tooltipRect.width / 2);
              break;
            case 'left':
              top = triggerRect.top + (triggerRect.height / 2) - (tooltipRect.height / 2);
              left = triggerRect.left - tooltipRect.width - 10;
              break;
            case 'right':
              top = triggerRect.top + (triggerRect.height / 2) - (tooltipRect.height / 2);
              left = triggerRect.right + 10;
              break;
          }
          
          tooltip.style.top = `${top + window.scrollY}px`;
          tooltip.style.left = `${left + window.scrollX}px`;
          tooltip.style.opacity = '1';
        });
        
        trigger.addEventListener('mouseleave', () => {
          const tooltip = document.querySelector('.tooltip');
          if (tooltip) {
            tooltip.remove();
          }
        });
      });
    }
    
    // Quantity selector functionality
    function initializeQuantitySelectors() {
      const quantitySelectors = document.querySelectorAll('.quantity-selector');
      
      quantitySelectors.forEach(selector => {
        const decreaseButton = selector.querySelector('.quantity-decrease');
        const increaseButton = selector.querySelector('.quantity-increase');
        const input = selector.querySelector('.quantity-input');
        
        if (!decreaseButton || !increaseButton || !input) return;
        
        decreaseButton.addEventListener('click', () => {
          const currentValue = parseInt(input.value);
          if (currentValue > 1) {
            input.value = currentValue - 1;
            input.dispatchEvent(new Event('change'));
          }
        });
        
        increaseButton.addEventListener('click', () => {
          const currentValue = parseInt(input.value);
          const max = input.getAttribute('max') ? parseInt(input.getAttribute('max')) : null;
          
          if (!max || currentValue < max) {
            input.value = currentValue + 1;
            input.dispatchEvent(new Event('change'));
          }
        });
      });
    }
    
    // Product options functionality
    function initializeProductOptions() {
      const optionSelectors = document.querySelectorAll('.option-selector');
      
      optionSelectors.forEach(selector => {
        const options = selector.querySelectorAll('.option-value');
        
        options.forEach(option => {
          option.addEventListener('click', () => {
            // Remove active class from all options
            options.forEach(opt => opt.classList.remove('active'));
            
            // Add active class to selected option
            option.classList.add('active');
            
            // Update hidden input value
            const hiddenInput = selector.querySelector('input[type="hidden"]');
            if (hiddenInput) {
              hiddenInput.value = option.getAttribute('data-value');
              hiddenInput.dispatchEvent(new Event('change'));
            }
          });
        });
      });
    }
    
    // Quick view functionality
    function initializeQuickView() {
      const quickViewButtons = document.querySelectorAll('.quick-view-button');
      
      quickViewButtons.forEach(button => {
        button.addEventListener('click', (e) => {
          e.preventDefault();
          
          const productUrl = button.getAttribute('data-product-url');
          const quickViewModal = document.getElementById('quickViewModal');
          const quickViewContent = document.getElementById('quickViewContent');
          
          if (quickViewModal && quickViewContent) {
            // Show loading state
            quickViewContent.innerHTML = '<div class="text-center py-10"><div class="spinner"></div><p>Loading product...</p></div>';
            quickViewModal.classList.remove('hidden');
            
            // Fetch product data
            fetch(`${productUrl}?view=quick-view`)
              .then(response => response.text())
              .then(html => {
                quickViewContent.innerHTML = html;
                
                // Initialize product functionality in quick view
                const quickViewForm = quickViewContent.querySelector('.product-form');
                if (quickViewForm) {
                  initializeProductOptions();
                  initializeQuantitySelectors();
                  
                  // Initialize product image slider
                  initializeSliders();
                }
              })
              .catch(error => {
                quickViewContent.innerHTML = '<div class="text-center py-10"><p>Error loading product. Please try again.</p></div>';
              });
          }
        });
      });
    }
    
    // Sticky add to cart functionality
    function initializeStickyAddToCart() {
      const productForm = document.querySelector('.product-form');
      const stickyAddToCart = document.getElementById('stickyAddToCart');
      
      if (productForm && stickyAddToCart) {
        const productFormObserver = new IntersectionObserver((entries) => {
          entries.forEach(entry => {
            if (!entry.isIntersecting) {
              stickyAddToCart.classList.remove('hidden');
            } else {
              stickyAddToCart.classList.add('hidden');
            }
          });
        }, { threshold: 0 });
        
        productFormObserver.observe(productForm);
      }
    }
    
    // Ajax cart functionality
    function initializeAjaxCart() {
      const addToCartForms = document.querySelectorAll('form[action="/cart/add"]');
      
      addToCartForms.forEach(form => {
        form.addEventListener('submit', (e) => {
          e.preventDefault();
          
          const formData = new FormData(form);
          
          fetch('/cart/add.js', {
            method: 'POST',
            body: formData
          })
          .then(response => response.json())
          .then(data => {
            // Update cart count
            updateCartCount();
            
            // Show cart notification
            showCartNotification(data);
          })
          .catch(error => {
            console.error('Error:', error);
            showCartNotification({ error: true, message: 'Error adding item to cart' });
          });
        });
      });
      
      function updateCartCount() {
        fetch('/cart.js')
          .then(response => response.json())
          .then(cart => {
            const cartCountElements = document.querySelectorAll('.cart-count');
            cartCountElements.forEach(element => {
              element.textContent = cart.item_count;
            });
          });
      }
      
      function showCartNotification(data) {
        const notification = document.getElementById('cartNotification');
        const notificationContent = document.getElementById('cartNotificationContent');
        
        if (notification && notificationContent) {
          if (data.error) {
            notificationContent.innerHTML = `<div class="text-error">${data.message || 'Error adding item to cart'}</div>`;
          } else {
            notificationContent.innerHTML = `
              <div class="flex items-center">
                <div class="mr-3">
                  <svg class="w-6 h-6 text-success" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                  </svg>
                </div>
                <div>
                  <p class="font-medium">Item added to cart</p>
                  <p class="text-sm">${data.product_title || 'Product'}</p>
                </div>
              </div>
              <div class="mt-3 flex justify-between">
                <a href="/cart" class="text-primary">View cart</a>
                <button type="button" class="text-gray-500" onclick="document.getElementById('cartNotification').classList.add('hidden')">Close</button>
              </div>
            `;
          }
          
          notification.classList.remove('hidden');
          
          // Auto-hide notification after 5 seconds
          setTimeout(() => {
            notification.classList.add('hidden');
          }, 5000);
        }
      }
    }
  </script>
  
  <!-- Additional scripts from settings -->
  {% if settings.additional_scripts %}
    {{ settings.additional_scripts }}
  {% endif %}
</body>
</html>

<!-- sections/header.liquid - Customizable header section -->
<header class="site-header {% if section.settings.sticky_header %}sticky top-0 z-50{% endif %}" style="background-color: {{ section.settings.header_bg_color }};">
  <div class="container mx-auto px-4 py-3">
    <div class="flex justify-between items-center">
      <!-- Logo -->
      <div class="flex items-center">
        {% if section.settings.logo != blank %}
          <a href="/" class="block">
            <img src="{{ section.settings.logo | img_url: 'medium' }}" alt="{{ shop.name }}" class="max-h-12">
          </a>
        {% else %}
          <a href="/" class="text-3xl font-bold {% if settings.theme_style == 'y2k' %}y2k-text{% endif %}" style="font-family: var(--heading-font);">
            {{ shop.name }}
            {% if section.settings.show_heart_icon and settings.theme_style == 'y2k' %}
            <span class="chrome-heart text-xl ml-1">♥</span>
            {% endif %}
          </a>
        {% endif %}
      </div>
      
      <!-- Navigation -->
      <div class="hidden md:flex space-x-8">
        {% for link in section.settings.menu.links %}
          {% if link.links.size > 0 %}
            <div class="relative group">
              <a href="{{ link.url }}" class="nav-link text-{{ section.settings.text_color }} hover:text-{{ section.settings.hover_color }}">
                {{ link.title }}
                <i class="fas fa-chevron-down ml-1 text-xs"></i>
              </a>
              <div class="absolute left-0 mt-2 w-48 bg-{{ section.settings.dropdown_bg_color }} rounded-md shadow-lg opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-300 z-10">
                <div class="py-2">
                  {% for childlink in link.links %}
                    <a href="{{ childlink.url }}" class="block px-4 py-2 text-{{ section.settings.dropdown_text_color }} hover:text-{{ section.settings.dropdown_hover_color }} hover:bg-opacity-10">
                      {{ childlink.title }}
                    </a>
                  {% endfor %}
                </div>
              </div>
            </div>
          {% else %}
            <a href="{{ link.url }}" class="nav-link text-{{ section.settings.text_color }} hover:text-{{ section.settings.hover_color }}">
              {{ link.title }}
            </a>
          {% endif %}
        {% endfor %}
      </div>
      
      <!-- Header Actions -->
      <div class="flex items-center space-x-4">
        {% if section.settings.show_search %}
          <a href="{{ routes.search_url }}" class="text-{{ section.settings.text_color }} hover:text-{{ section.settings.hover_color }}">
            <i class="fas fa-search"></i>
          </a>
        {% endif %}
        
        {% if section.settings.show_account %}
          <a href="{{ routes.account_url }}" class="text-{{ section.settings.text_color }} hover:text-{{ section.settings.hover_color }}">
            <i class="fas fa-user"></i>
          </a>
        {% endif %}
        
        {% if section.settings.show_cart %}
          <a href="{{ routes.cart_url }}" class="text-{{ section.settings.text_color }} hover:text-{{ section.settings.hover_color }} relative">
            <i class="fas fa-shopping-bag"></i>
            <span class="cart-count absolute -top-2 -right-2 bg-{{ section.settings.cart_badge_color }} text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">
              {{ cart.item_count }}
            </span>
          </a>
        {% endif %}
        
        <button class="md:hidden text-{{ section.settings.text_color }}" id="mobileMenuButton">
          <i class="fas fa-bars"></i>
        </button>
      </div>
    </div>
    
    <!-- Mobile Menu -->
    <div id="mobileMenu" class="hidden md:hidden mt-4 pb-4">
      <div class="flex flex-col space-y-3">
        {% for link in section.settings.menu.links %}
          {% if link.links.size > 0 %}
            <div class="mobile-dropdown">
              <button class="flex justify-between items-center w-full text-{{ section.settings.text_color }} hover:text-{{ section.settings.hover_color }} font-accent" data-toggle="mobile-submenu-{{ forloop.index }}">
                {{ link.title }}
                <i class="fas fa-chevron-down ml-1 text-xs"></i>
              </button>
              <div id="mobile-submenu-{{ forloop.index }}" class="hidden pl-4 mt-2 space-y-2">
                {% for childlink in link.links %}
                  <a href="{{ childlink.url }}" class="block text-{{ section.settings.text_color }} hover:text-{{ section.settings.hover_color }} font-accent">
                    {{ childlink.title }}
                  </a>
                {% endfor %}
              </div>
            </div>
          {% else %}
            <a href="{{ link.url }}" class="text-{{ section.settings.text_color }} hover:text-{{ section.settings.hover_color }} font-accent">
              {{ link.title }}
            </a>
          {% endif %}
        {% endfor %}
      </div>
    </div>
  </div>
</header>

<style>
  .nav-link {
    position: relative;
    font-family: var(--accent-font);
    letter-spacing: var(--letter-spacing);
  }
  
  .nav-link::after {
    content: '';
    position: absolute;
    width: 0;
    height: 2px;
    bottom: -2px;
    left: 0;
    background: linear-gradient(to right, var(--primary-color), var(--secondary-color));
    transition: width var(--animation-speed) var(--transition-timing);
  }
  
  .nav-link:hover::after {
    width: 100%;
  }
  
  .sticky {
    position: sticky;
    backdrop-filter: blur(10px);
  }
</style>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    // Mobile dropdown toggles
    const mobileDropdowns = document.querySelectorAll('.mobile-dropdown button');
    mobileDropdowns.forEach(button => {
      button.addEventListener('click', function() {
        const targetId = this.getAttribute('data-toggle');
        const submenu = document.getElementById(targetId);
        submenu.classList.toggle('hidden');
        this.querySelector('i').classList.toggle('fa-chevron-down');
        this.querySelector('i').classList.toggle('fa-chevron-up');
      });
    });
  });
</script>

{% schema %}
{
  "name": "Header",
  "settings": [
    {
      "type": "image_picker",
      "id": "logo",
      "label": "Logo"
    },
    {
      "type": "checkbox",
      "id": "show_heart_icon",
      "label": "Show heart icon next to logo",
      "default": true,
      "info": "Only applies when using text logo in Y2K theme style"
    },
    {
      "type": "link_list",
      "id": "menu",
      "label": "Menu",
      "default": "main-menu"
    },
    {
      "type": "checkbox",
      "id": "sticky_header",
      "label": "Sticky header",
      "default": true
    },
    {
      "type": "color",
      "id": "header_bg_color",
      "label": "Background color",
      "default": "#111111"
    },
    {
      "type": "select",
      "id": "text_color",
      "label": "Text color",
      "options": [
        {
          "value": "white",
          "label": "White"
        },
        {
          "value": "gray-300",
          "label": "Light Gray"
        },
        {
          "value": "primary",
          "label": "Primary Color"
        }
      ],
      "default": "white"
    },
    {
      "type": "select",
      "id": "hover_color",
      "label": "Hover color",
      "options": [
        {
          "value": "white",
          "label": "White"
        },
        {
          "value": "primary",
          "label": "Primary Color"
        },
        {
          "value": "secondary",
          "label": "Secondary Color"
        }
      ],
      "default": "primary"
    },
    {
      "type": "color",
      "id": "dropdown_bg_color",
      "label": "Dropdown background color",
      "default": "#111111"
    },
    {
      "type": "select",
      "id": "dropdown_text_color",
      "label": "Dropdown text color",
      "options": [
        {
          "value": "white",
          "label": "White"
        },
        {
          "value": "gray-300",
          "label": "Light Gray"
        }
      ],
      "default": "white"
    },
    {
      "type": "select",
      "id": "dropdown_hover_color",
      "label": "Dropdown hover color",
      "options": [
        {
          "value": "white",
          "label": "White"
        },
        {
          "value": "primary",
          "label": "Primary Color"
        }
      ],
      "default": "primary"
    },
    {
      "type": "checkbox",
      "id": "show_search",
      "label": "Show search icon",
      "default": true
    },
    {
      "type": "checkbox",
      "id": "show_account",
      "label": "Show account icon",
      "default": true
    },
    {
      "type": "checkbox",
      "id": "show_cart",
      "label": "Show cart icon",
      "default": true
    },
    {
      "type": "select",
      "id": "cart_badge_color",
      "label": "Cart badge color",
      "options": [
        {
          "value": "primary",
          "label": "Primary Color"
        },
        {
          "value": "secondary",
          "label": "Secondary Color"
        },
        {
          "value": "accent",
          "label": "Accent Color"
        }
      ],
      "default": "primary"
    }
  ],
  "presets": [
    {
      "name": "Header",
      "category": "Header"
    }
  ]
}
{% endschema %}

<!-- sections/footer.liquid - Customizable footer section -->
<footer class="site-footer py-16" style="background-color: {{ section.settings.footer_bg_color }}; color: {{ section.settings.footer_text_color }}; border-top: 1px solid {{ section.settings.footer_border_color }};">
  <div class="container mx-auto px-4">
    <div class="grid grid-cols-1 md:grid-cols-{{ section.settings.column_count }} gap-10">
      <!-- Brand Column -->
      <div>
        <h3 class="text-2xl font-bold mb-6 {% if section.settings.use_gradient_text and settings.theme_style == 'y2k' %}y2k-text{% endif %}" style="font-family: var(--heading-font);">
          {{ section.settings.brand_title | default: shop.name }}
          {% if section.settings.show_heart_icon and settings.theme_style == 'y2k' %}
          <span class="chrome-heart">♥</span>
          {% endif %}
        </h3>
        
        <p class="mb-6" style="font-family: var(--body-font); color: {{ section.settings.footer_text_color }};">
          {{ section.settings.brand_description }}
        </p>
        
        {% if section.settings.show_social_icons %}
        <div class="flex space-x-4">
          {% if settings.social_instagram_link != blank %}
            <a href="{{ settings.social_instagram_link }}" class="text-{{ section.settings.social_icon_color }} hover:text-{{ section.settings.social_icon_hover_color }}">
              <i class="fab fa-instagram"></i>
            </a>
          {% endif %}
          
          {% if settings.social_facebook_link != blank %}
            <a href="{{ settings.social_facebook_link }}" class="text-{{ section.settings.social_icon_color }} hover:text-{{ section.settings.social_icon_hover_color }}">
              <i class="fab fa-facebook-f"></i>
            </a>
          {% endif %}
          
          {% if settings.social_twitter_link != blank %}
            <a href="{{ settings.social_twitter_link }}" class="text-{{ section.settings.social_icon_color }} hover:text-{{ section.settings.social_icon_hover_color }}">
              <i class="fab fa-twitter"></i>
            </a>
          {% endif %}
          
          {% if settings.social_pinterest_link != blank %}
            <a href="{{ settings.social_pinterest_link }}" class="text-{{ section.settings.social_icon_color }} hover:text-{{ section.settings.social_icon_hover_color }}">
              <i class="fab fa-pinterest-p"></i>
            </a>
          {% endif %}
          
          {% if settings.social_tiktok_link != blank %}
            <a href="{{ settings.social_tiktok_link }}" class="text-{{ section.settings.social_icon_color }} hover:text-{{ section.settings.social_icon_hover_color }}">
              <i class="fab fa-tiktok"></i>
            </a>
          {% endif %}
          
          {% if settings.social_youtube_link != blank %}
            <a href="{{ settings.social_youtube_link }}" class="text-{{ section.settings.social_icon_color }} hover:text-{{ section.settings.social_icon_hover_color }}">
              <i class="fab fa-youtube"></i>
            </a>
          {% endif %}
        </div>
        {% endif %}
      </div>
      
      <!-- Menu Columns -->
      {% for block in section.blocks %}
        {% if block.type == 'link_list' %}
          <div>
            <h4 class="text-lg font-semibold mb-6" style="font-family: var(--accent-font); color: {{ section.settings.footer_heading_color }};">
              {{ block.settings.title | upcase }}
            </h4>
            
            {% if block.settings.menu != blank %}
              <ul class="space-y-3">
                {% for link in block.settings.menu.links %}
                  <li>
                    <a href="{{ link.url }}" class="text-{{ section.settings.footer_link_color }} hover:text-{{ section.settings.footer_link_hover_color }}" style="font-family: var(--body-font);">
                      {{ link.title }}
                    </a>
                  </li>
                {% endfor %}
              </ul>
            {% endif %}
          </div>
        {% endif %}
        
        {% if block.type == 'text' %}
          <div>
            <h4 class="text-lg font-semibold mb-6" style="font-family: var(--accent-font); color: {{ section.settings.footer_heading_color }};">
              {{ block.settings.title | upcase }}
            </h4>
            
            <div class="text-{{ section.settings.footer_text_color }}" style="font-family: var(--body-font);">
              {{ block.settings.text }}
            </div>
          </div>
        {% endif %}
        
        {% if block.type == 'newsletter' %}
          <div>
            <h4 class="text-lg font-semibold mb-6" style="font-family: var(--accent-font); color: {{ section.settings.footer_heading_color }};">
              {{ block.settings.title | upcase }}
            </h4>
            
            <p class="mb-4 text-{{ section.settings.footer_text_color }}" style="font-family: var(--body-font);">
              {{ block.settings.text }}
            </p>
            
            {% form 'customer', id: 'footer-newsletter-form' %}
              <input type="hidden" name="contact[tags]" value="newsletter">
              <div class="flex flex-col sm:flex-row gap-2">
                <input type="email" name="contact[email]" placeholder="{{ block.settings.placeholder }}" 
                       class="px-4 py-2 rounded-full bg-white/10 border border-white/30 text-white placeholder-gray-300 focus:outline-none focus:ring-2 w-full" 
                       style="font-family: var(--body-font); --tw-ring-color: var(--primary-color);" 
                       required>
                <button type="submit" class="theme-button text-white py-2 px-6 rounded-full transition duration-300 text-sm">
                  {{ block.settings.button_text | upcase }}
                </button>
              </div>
            {% endform %}
          </div>
        {% endif %}
      {% endfor %}
    </div>
    
    <!-- Bottom Footer -->
    <div class="border-t mt-16 pt-10 text-center" style="border-color: {{ section.settings.footer_divider_color }};">
      <p class="text-{{ section.settings.footer_text_color }}" style="font-family: var(--body-font);">
        {{ section.settings.copyright_text | default: '&copy; 2023 ' | append: shop.name | append: '. All rights reserved.' }}
      </p>
      
      {% if section.settings.show_payment_icons %}
        <div class="mt-4 flex justify-center space-x-2">
          {% for type in shop.enabled_payment_types %}
            {{ type | payment_type_svg_tag: class: 'h-8 w-auto' }}
          {% endfor %}
        </div>
      {% endif %}
    </div>
  </div>
</footer>

{% schema %}
{
  "name": "Footer",
  "settings": [
    {
      "type": "color",
      "id": "footer_bg_color",
      "label": "Background color",
      "default": "#111111"
    },
    {
      "type": "color",
      "id": "footer_text_color",
      "label": "Text color",
      "default": "#9ca3af"
    },
    {
      "type": "color",
      "id": "footer_heading_color",
      "label": "Heading color",
      "default": "#ffffff"
    },
    {
      "type": "color",
      "id": "footer_border_color",
      "label": "Border color",
      "default": "#1f2937"
    },
    {
      "type": "color",
      "id": "footer_divider_color",
      "label": "Divider color",
      "default": "#1f2937"
    },
    {
      "type": "select",
      "id": "footer_link_color",
      "label": "Link color",
      "options": [
        {
          "value": "gray-400",
          "label": "Light Gray"
        },
        {
          "value": "white",
          "label": "White"
        },
        {
          "value": "primary",
          "label": "Primary Color"
        }
      ],
      "default": "gray-400"
    },
    {
      "type": "select",
      "id": "footer_link_hover_color",
      "label": "Link hover color",
      "options": [
        {
          "value": "white",
          "label": "White"
        },
        {
          "value": "primary",
          "label": "Primary Color"
        },
        {
          "value": "secondary",
          "label": "Secondary Color"
        }
      ],
      "default": "primary"
    },
    {
      "type": "range",
      "id": "column_count",
      "label": "Column count",
      "min": 2,
      "max": 5,
      "step": 1,
      "default": 4
    },
    {
      "type": "text",
      "id": "brand_title",
      "label": "Brand title",
      "default": "Your Brand"
    },
    {
      "type": "checkbox",
      "id": "use_gradient_text",
      "label": "Use gradient text for brand title",
      "default": true,
      "info": "Only applies when using Y2K theme style"
    },
    {
      "type": "checkbox",
      "id": "show_heart_icon",
      "label": "Show heart icon",
      "default": true,
      "info": "Only applies when using Y2K theme style"
    },
    {
      "type": "textarea",
      "id": "brand_description",
      "label": "Brand description",
      "default": "Your brand description goes here. Share your mission, values, or a brief overview of what your brand stands for."
    },
    {
      "type": "checkbox",
      "id": "show_social_icons",
      "label": "Show social icons",
      "default": true
    },
    {
      "type": "select",
      "id": "social_icon_color",
      "label": "Social icon color",
      "options": [
        {
          "value": "gray-400",
          "label": "Light Gray"
        },
        {
          "value": "white",
          "label": "White"
        },
        {
          "value": "primary",
          "label": "Primary Color"
        }
      ],
      "default": "gray-400"
    },
    {
      "type": "select",
      "id": "social_icon_hover_color",
      "label": "Social icon hover color",
      "options": [
        {
          "value": "white",
          "label": "White"
        },
        {
          "value": "primary",
          "label": "Primary Color"
        },
        {
          "value": "secondary",
          "label": "Secondary Color"
        }
      ],
      "default": "primary"
    },
    {
      "type": "text",
      "id": "copyright_text",
      "label": "Copyright text",
      "default": "&copy; 2023 Your Brand. All rights reserved."
    },
    {
      "type": "checkbox",
      "id": "show_payment_icons",
      "label": "Show payment icons",
      "default": true
    }
  ],
  "blocks": [
    {
      "type": "link_list",
      "name": "Menu",
      "settings": [
        {
          "type": "text",
          "id": "title",
          "label": "Title",
          "default": "Quick links"
        },
        {
          "type": "link_list",
          "id": "menu",
          "label": "Menu"
        }
      ]
    },
    {
      "type": "text",
      "name": "Text",
      "settings": [
        {
          "type": "text",
          "id": "title",
          "label": "Title",
          "default": "Our mission"
        },
        {
          "type": "richtext",
          "id": "text",
          "label": "Text",
          "default": "<p>Share information about your brand, product, or services with your customers.</p>"
        }
      ]
    },
    {
      "type": "newsletter",
      "name": "Newsletter",
      "limit": 1,
      "settings": [
        {
          "type": "text",
          "id": "title",
          "label": "Title",
          "default": "Subscribe"
        },
        {
          "type": "richtext",
          "id": "text",
          "label": "Text",
          "default": "<p>Subscribe to get special offers, free giveaways, and once-in-a-lifetime deals.</p>"
        },
        {
          "type": "text",
          "id": "placeholder",
          "label": "Email placeholder text",
          "default": "Your email"
        },
        {
          "type": "text",
          "id": "button_text",
          "label": "Button text",
          "default": "Subscribe"
        }
      ]
    }
  ],
  "presets": [
    {
      "name": "Footer",
      "blocks": [
        {
          "type": "link_list"
        },
        {
          "type": "link_list"
        },
        {
          "type": "newsletter"
        }
      ]
    }
  ]
}
{% endschema %}

<!-- sections/announcement-bar.liquid - Customizable announcement bar -->
<div class="announcement-bar py-2 text-center" style="background-color: {{ section.settings.bg_color }}; color: {{ section.settings.text_color }};">
  <div class="container mx-auto px-4">
    {% if section.blocks.size > 0 %}
      <div class="announcement-slider" data-autoplay="{{ section.settings.autoplay }}" data-speed="{{ section.settings.rotation_speed }}">
        {% for block in section.blocks %}
          <div class="announcement-slide">
            {% if block.settings.link != blank %}
              <a href="{{ block.settings.link }}" class="inline-flex items-center" style="color: {{ section.settings.text_color }};">
                {% if block.settings.icon != blank %}
                  <span class="mr-2">{{ block.settings.icon }}</span>
                {% endif %}
                {{ block.settings.text }}
                {% if block.settings.show_arrow %}
                  <span class="ml-2">→</span>
                {% endif %}
              </a>
            {% else %}
              <div class="inline-flex items-center">
                {% if block.settings.icon != blank %}
                  <span class="mr-2">{{ block.settings.icon }}</span>
                {% endif %}
                {{ block.settings.text }}
              </div>
            {% endif %}
          </div>
        {% endfor %}
      </div>
    {% else %}
      <p>Add announcement messages from the section editor</p>
    {% endif %}
  </div>
  
  {% if section.settings.show_close_button %}
    <button class="absolute right-4 top-1/2 transform -translate-y-1/2 text-{{ section.settings.text_color }} opacity-70 hover:opacity-100" data-announcement-close>
      <i class="fas fa-times"></i>
    </button>
  {% endif %}
</div>

<style>
  .announcement-slider {
    position: relative;
    overflow: hidden;
  }
  
  .announcement-slide {
    display: none;
    animation: fadeInOut 0.5s ease-in-out;
  }
  
  .announcement-slide.active {
    display: block;
  }
  
  @keyframes fadeInOut {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }
</style>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    const slider = document.querySelector('.announcement-slider');
    if (!slider) return;
    
    const slides = slider.querySelectorAll('.announcement-slide');
    if (slides.length <= 0) return;
    
    // Show first slide
    slides[0].classList.add('active');
    
    // Set up rotation if more than one slide
    if (slides.length > 1 && slider.getAttribute('data-autoplay') === 'true') {
      let currentSlide = 0;
      const speed = parseInt(slider.getAttribute('data-speed')) * 1000 || 5000;
      
      setInterval(() => {
        slides[currentSlide].classList.remove('active');
        currentSlide = (currentSlide + 1) % slides.length;
        slides[currentSlide].classList.add('active');
      }, speed);
    }
    
    // Close button functionality
    const closeButton = document.querySelector('[data-announcement-close]');
    if (closeButton) {
      closeButton.addEventListener('click', function() {
        const announcementBar = this.closest('.announcement-bar');
        announcementBar.style.display = 'none';
        
        // Save to session storage to keep it closed
        sessionStorage.setItem('announcement-bar-closed', 'true');
      });
      
      // Check if previously closed
      if (sessionStorage.getItem('announcement-bar-closed') === 'true') {
        document.querySelector('.announcement-bar').style.display = 'none';
      }
    }
  });
</script>

{% schema %}
{
  "name": "Announcement Bar",
  "settings": [
    {
      "type": "color",
      "id": "bg_color",
      "label": "Background color",
      "default": "#000000"
    },
    {
      "type": "color",
      "id": "text_color",
      "label": "Text color",
      "default": "#ffffff"
    },
    {
      "type": "checkbox",
      "id": "autoplay",
      "label": "Auto-rotate announcements",
      "default": true
    },
    {
      "type": "range",
      "id": "rotation_speed",
      "label": "Rotation speed (seconds)",
      "min": 3,
      "max": 10,
      "step": 1,
      "default": 5
    },
    {
      "type": "checkbox",
      "id": "show_close_button",
      "label": "Show close button",
      "default": true
    }
  ],
  "blocks": [
    {
      "type": "announcement",
      "name": "Announcement",
      "settings": [
        {
          "type": "text",
          "id": "text",
          "label": "Text",
          "default": "Announce something here"
        },
        {
          "type": "text",
          "id": "icon",
          "label": "Icon",
          "info": "Enter emoji or icon code"
        },
        {
          "type": "url",
          "id": "link",
          "label": "Link"
        },
        {
          "type": "checkbox",
          "id": "show_arrow",
          "label": "Show arrow",
          "default": false
        }
      ]
    }
  ],
  "presets": [
    {
      "name": "Announcement Bar",
      "blocks": [
        {
          "type": "announcement"
        }
      ]
    }
  ]
}
{% endschema %}

<!-- sections/hero.liquid - Customizable hero section -->
<section class="hero-section relative {% if section.settings.full_height %}min-h-screen{% else %}py-32{% endif %} flex items-center" 
         style="background-color: {{ section.settings.bg_color }};">
  
  {% if section.settings.show_background_effects %}
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      {% if settings.theme_style == 'y2k' %}
        {% if section.settings.background_style == 'grid' or section.settings.background_style == 'both' %}
          <div class="absolute inset-0 y2k-grid"></div>
        {% endif %}
        
        {% if section.settings.background_style == 'bubbles' or section.settings.background_style == 'both' %}
          <div class="y2k-bubble w-32 h-32 absolute top-1/4 left-1/6"></div>
          <div class="y2k-bubble w-24 h-24 absolute bottom-1/4 right-1/6"></div>
          <div class="y2k-bubble w-40 h-40 absolute top-1/2 right-1/4"></div>
        {% endif %}
      {% else %}
        <div class="absolute inset-0 bg-pattern opacity-10"></div>
      {% endif %}
    </div>
  {% endif %}
  
  <div class="container mx-auto px-4 relative z-10">
    <div class="flex flex-col {% if section.settings.content_alignment == 'center' %}items-center text-center{% elsif section.settings.content_alignment == 'right' %}items-end text-right{% else %}items-start text-left{% endif %}">
      {% if section.settings.overline != blank %}
        <div class="mb-4 {% if settings.theme_style == 'y2k' and section.settings.use_gradient_text %}y2k-text{% endif %}" style="font-family: var(--accent-font);">
          {{ section.settings.overline }}
        </div>
      {% endif %}
      
      <h1 class="text-4xl md:text-6xl lg:text-7xl font-bold mb-6 max-w-3xl {% if settings.theme_style == 'y2k' and section.settings.use_gradient_text %}y2k-text{% endif %}" style="font-family: var(--heading-font);">
        {{ section.settings.heading }}
        {% if section.settings.show_heart_icon and settings.theme_style == 'y2k' %}
          <span class="chrome-heart">♥</span>
        {% endif %}
      </h1>
      
      {% if section.settings.subheading != blank %}
        <div class="text-xl md:text-2xl mb-8 max-w-2xl" style="font-family: var(--body-font); color: {{ section.settings.text_color }};">
          {{ section.settings.subheading }}
        </div>
      {% endif %}
      
      {% if section.settings.show_buttons %}
        <div class="flex flex-wrap gap-4 mt-4">
          {% if section.settings.button1_text != blank %}
            <a href="{{ section.settings.button1_link }}" class="theme-button">
              {{ section.settings.button1_text | upcase }}
            </a>
          {% endif %}
          
          {% if section.settings.button2_text != blank %}
            <a href="{{ section.settings.button2_link }}" class="border-2 border-{{ section.settings.button2_color }} text-{{ section.settings.button2_text_color }} hover:bg-{{ section.settings.button2_color }} hover:text-white py-3 px-10 rounded-full transition duration-300" style="font-family: var(--accent-font);">
              {{ section.settings.button2_text | upcase }}
            </a>
          {% endif %}
        </div>
      {% endif %}
    </div>
  </div>
  
  {% if section.settings.show_image and section.settings.image != blank %}
    <div class="absolute {% if section.settings.image_position == 'right' %}right-0{% else %}left-0{% endif %} top-0 h-full w-1/2 overflow-hidden hidden lg:block">
      <img src="{{ section.settings.image | img_url: 'master' }}" alt="{{ section.settings.heading }}" class="object-cover h-full w-full">
      {% if section.settings.show_image_overlay %}
        <div class="absolute inset-0" style="background: linear-gradient(to {{ section.settings.image_position }}, transparent, {{ section.settings.bg_color }});"></div>
      {% endif %}
    </div>
  {% endif %}
</section>

{% schema %}
{
  "name": "Hero Section",
  "settings": [
    {
      "type": "text",
      "id": "overline",
      "label": "Overline text",
      "default": "NEW COLLECTION"
    },
    {
      "type": "text",
      "id": "heading",
      "label": "Heading",
      "default": "Your Brand Headline"
    },
    {
      "type": "textarea",
      "id": "subheading",
      "label": "Subheading",
      "default": "A brief description of your brand, product, or promotion."
    },
    {
      "type": "checkbox",
      "id": "use_gradient_text",
      "label": "Use gradient text",
      "default": true,
      "info": "Only applies when using Y2K theme style"
    },
    {
      "type": "checkbox",
      "id": "show_heart_icon",
      "label": "Show heart icon",
      "default": true,
      "info": "Only applies when using Y2K theme style"
    },
    {
      "type": "color",
      "id": "bg_color",
      "label": "Background color",
      "default": "#111111"
    },
    {
      "type": "color",
      "id": "text_color",
      "label": "Text color",
      "default": "#ffffff"
    },
    {
      "type": "select",
      "id": "content_alignment",
      "label": "Content alignment",
      "options": [
        {
          "value": "left",
          "label": "Left"
        },
        {
          "value": "center",
          "label": "Center"
        },
        {
          "value": "right",
          "label": "Right"
        }
      ],
      "default": "left"
    },
    {
      "type": "checkbox",
      "id": "full_height",
      "label": "Full height section",
      "default": true
    },
    {
      "type": "checkbox",
      "id": "show_background_effects",
      "label": "Show background effects",
      "default": true
    },
    {
      "type": "select",
      "id": "background_style",
      "label": "Background style",
      "options": [
        {
          "value": "grid",
          "label": "Grid"
        },
        {
          "value": "bubbles",
          "label": "Bubbles"
        },
        {
          "value": "both",
          "label": "Grid and Bubbles"
        },
        {
          "value": "none",
          "label": "None"
        }
      ],
      "default": "both",
      "info": "Only applies when using Y2K theme style"
    },
    {
      "type": "header",
      "content": "Buttons"
    },
    {
      "type": "checkbox",
      "id": "show_buttons",
      "label": "Show buttons```
