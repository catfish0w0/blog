---
# Mr. Green Jekyll Theme (https://github.com/MrGreensWorkshop/MrGreen-JekyllTheme)
# Copyright (c) 2022 Mr. Green's Workshop https://www.MrGreensWorkshop.com
# Licensed under MIT

layout: default
# About page
---

{%- include multi_lng/get-lng-by-url.liquid -%}
{%- assign lng = get_lng -%}

<div class="multipurpose-container about-container">
  <div class="row about-main">
    <div class="col-md-3 about-img">
      <img src="{{ page.img }}" alt="">
    </div>
    <div class="col-md-9 about-header">
      <h1 translate="no">{{ site.data.owner[lng].brand }}</h1>
      <div class="meta-container">
        {%- assign about_title = site.data.owner[lng].about.sub_title | replace: site.data.conf.main.sample_replace, site.data.lang[lng].constants.sample -%}
        {%- if site.data.owner[lng].about.sub_title %}
          <p class="sub-title">
            {%- if site.data.conf.others.about.sub_title_icon %}<i class="{{ 'fa-fw ' }}{{ site.data.conf.others.about.sub_title_icon }}" aria-hidden="true"></i>{% endif -%}
            &nbsp;{{ about_title }}
          </p>
        {% endif -%}
        {%- assign tmp_obj =  site.data.owner[lng].contacts | where_exp: "item", "item.email != nil" | first -%}
        {%- assign email = tmp_obj['email'] -%}
        {%- if site.data.conf.others.about.show_email and email %}
          {%- assign _email = email | split: '@' %}
          <p class="email">
            <a href="javascript:void(0);" onclick="setAddress('{{ _email[0] }}', '{{ _email[1] }}');">
              {%- if site.data.conf.others.about.email_icon %}<i class="{{ 'fa-fw ' }}{{ site.data.conf.others.about.email_icon }}"></i>{% endif -%}
              &nbsp;{{ site.data.lang[lng].about.email_title }}
            </a>
          </p>
        {% endif -%}
        {%- if site.data.conf.others.about.show_contacts and site.data.owner[lng].contacts.size > 0 %}
          {% include default/nav/contact-links.html -%}
        {% endif -%}
      </div>
    </div>
  </div>
  <div class="row about-divider">
    <hr>
  </div>
  <div class="row">
    <div class="col-md-12">
      <div class="about-msg markdown-style">
        <div class="center-container">
            <main class="row2 middle-xs about-container2">
                <div class="col-md-3a col-xs-12a about-left">
                  <h6>how it all started</h6>
                  <h4>The Story Behind and The Process</h4>
                </div>
                <div class="col-md-9a col-xs-12a about-right">
                  <p>
                      In 2017, I took my first dive into coding with an introductory Java course at Tacoma Community College. While it didn't immediately ignite a strong passion within me, it left a positive impression of the coding industry and sparked my curiosity to explore more CS classes during my time at UCLA.
                      <br>
                      <br>
                      After transferring to UCLA as a chemical engineering major, I had the opportunity to participate in internships and research experiences within the chemical engineering field. However, my fascination with computer science persisted, prompting me to enroll in courses such as CS 31, CS 32, and CS 33 at UCLA. These courses allowed me to immerse myself in the captivating world of algorithms and software design.
                  </p>
                </div>
                <div class="col-md-3a col-xs-12a about-left">
                  <h6>Providing various services</h6>
                  <h4>Improving the web since 2013</h4>
                </div>
                <div class="col-md-9a col-xs-12a about-right">
                  <p>
                      Following my graduation, I secured a job as a System Engineer at an HVAC company in New York. While this position provided me with valuable skills and experiences in the HVAC industry, my interest in software engineering continued to flourish. I began self-studying Java once again and successfully built a couple of full-stack web applications using React for the frontend and Spring MVC and Go for the backend. These projects served as excellent preparation for my desired career shift.
                      <br>
                      <br>
                      Currently, I am pursuing a Master's degree in Computer Science at Georgia Tech, fully dedicated to expanding my knowledge and honing my skills in this exhilarating discipline. My studies are focused on advanced topics such as artificial intelligence, machine learning, and software architecture.
                      <br>
                      <br>
                      I am eager to further explore the limitless possibilities that computer science offers and apply my skills to solve real-world problems. With each step forward, I am excited to see where this journey takes me and how I can contribute to the ever-evolving field of technology.
                  </p>
                </div>
          </main>
        </div>
        {{ content }}
        {%- if site.data.conf.main.contact_form.enable and site.data.conf.others.about.show_contact_form_button %}
        <a href="javascript:void(0);" class="btn-base " onclick="ContactForm.show();" role="button">{{ site.data.lang[lng].contact_form.button_name }}</a>
        {% endif -%}
      </div>
    </div>
  </div>
</div>
