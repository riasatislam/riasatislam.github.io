---
# Leave the homepage title empty to use the site title
title: ""
date: 2024-09-19
type: landing

design:
  # Default section spacing
  spacing: "6rem"

sections:
  - block: resume-biography-3
    content:
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
      text: ""
      # Show a call-to-action button under your biography? (optional)
      button:
        text: Download CV
        url: uploads/resume.pdf
    design:
      css_class: dark
      background:
        color: black
        image:
          # Add your image background to `assets/media/`.
          filename: stacked-peaks.svg
          filters:
            brightness: 1.0
          size: cover
          position: center
          parallax: false

  - block: markdown
    content:
      title: 'Research'
      subtitle: ''
      text: |-
        Dr Riasat Islam's research interests focus on the intersection of Human-Computer Interaction (HCI) and Artificial Intelligence (AI). He is particularly passionate about developing user-centred AI systems with applications in healthcare and well-being, aiming to create solutions that enhance the user experience while supporting physical and mental health. 
        Additionally, Dr Islam is interested in exploring the use of user-centred AI in Islamic computing, with a focus on creating interconnected learning platforms that foster spiritual growth and well-being. 
        If you would like to work with Riasat and/or GTAF.org, please get in touch.
    design:
      columns: '1'

  - block: collection
    id: blog
    content:
      title: Blog Posts
      subtitle: ''
      text: ''
      page_type: blog
      count: 5
      filters:
        author: ""
        category: ""
        tag: ""
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ""
      offset: 0
      order: desc
    design: 
      view: date-title-summary
      spacing:
        padding: [0, 0, 0, 0]
    
#  - block: collection
#    id: papers
#    content:
#      title: Featured Publications
#      filters:
#        folders:
#          - publication
#        featured_only: true
#    design:
#      view: article-grid
#      columns: 2
#  - block: collection
#    content:
#      title: Recent Publications
#      text: ""
#      filters:
#        folders:
#          - publication
#        exclude_featured: false
#    design:
#      view: citation
#  - block: collection
#    id: talks
#    content:
#      title: Recent & Upcoming Talks
#      filters:
#        folders:
#          - event
#    design:
#      view: article-grid
#      columns: 1
# - block: collection
#   id: news
#   content:
#     title: Recent News
#     subtitle: ''
#     text: ''
#     # Page type to display. E.g. post, talk, publication...
#     page_type: post
#     # Choose how many pages you would like to display (0 = all pages)
#     count: 5
#     # Filter on criteria
#     filters:
#       author: ""
#       category: ""
#       tag: ""
#       exclude_featured: false
#       exclude_future: false
#       exclude_past: false
#       publication_type: ""
#    # Choose how many pages you would like to offset by
#     offset: 0
#     # Page order: descending (desc) or ascending (asc) date.
#     order: desc
#   design:
#     # Choose a layout view
#     view: date-title-summary
#     # Reduce spacing
#     spacing:
#       padding: [0, 0, 0, 0]
#  - block: cta-card
#    demo: true # Only display this section in the Hugo Blox Builder demo site
#    content:
#      title: 👉 Build your own academic website like this
#      text: |-
#        This site is generated by Hugo Blox Builder - the FREE, Hugo-based open source website builder trusted by 250,000+ academics like you.

#        <a class="github-button" href="https://github.com/HugoBlox/hugo-blox-builder" data-color-scheme="no-preference: light; light: light; dark: dark;" data-icon="octicon-star" data-size="large" data-show-count="true" aria-label="Star HugoBlox/hugo-blox-builder on GitHub">Star</a>

#        Easily build anything with blocks - no-code required!
#        
#        From landing pages, second brains, and courses to academic resumés, conferences, and tech blogs.
#      button:
#        text: Get Started
#        url: https://hugoblox.com/templates/
#    design:
#      card:
#        # Card background color (CSS class)
#        css_class: "bg-primary-700"
#        css_style: ""
---
