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
                      In 2017, I took my first dive into coding with an introductory Java course at Tacoma Community College. While it didn't immediately ignite a strong passion within me, it left me a great impression in coding and sparked my curiosity to explore more CS topics during my time at UCLA.
                      <br>
                      <br>
                      After transferring to UCLA as a chemical engineering major, I decided to take the plunge and enroll in some additional courses. I signed up for CS 31, CS 32, and CS 33 at UCLA. The courses itself were quite challenging! However, those courses provided me with a solid foundation in the realm of algorithms and software design.
                      <br>
                      <br>
                      Following my graduation, I secured a job as a System Engineer at an HVAC company in New York. While this position provided me with valuable engineering skills and experiences, my interest in software engineering continued to flourish. 
                      <br>
                      <br>
                      I began self-studying Java once again and successfully built a couple of full-stack web applications using React for the frontend and Spring MVC and Go for the backend. These projects served as excellent preparation for my desired career shift.
                  </p>
                </div>
                <div class="col-md-3a col-xs-12a about-left">
                  <h6>Continued Studying</h6>
                  <h4>Improving Myself as a Software Engineer</h4>
                </div>
                <div class="col-md-9a col-xs-12a about-right">
                  <p>
                      Currently, I am pursuing a Master's degree in Computer Science at Georgia Tech, fully dedicated to expanding my knowledge and honing my skills in this exhilarating discipline. I will be studying on other interesting topics such as <b>artificial intelligence</b>, <b>machine learning</b>, and <b>software architecture</b>.
                      <br>
                      <br>
                      I am eager to further explore the limitless possibilities that computer science offers and apply my skills to solve real-world problems. With each step forward, I am excited to see where this journey takes me and how I can contribute to the ever-evolving field of technology.
                      <br>
                      <br>
                      As mentioned above, I'm specialized in <b>HTML</b>, <b>CSS</b>, and <b>React JS</b> on the frontend. I'm also pretty comfortable with <b>Spring MVC</b>, <b>Spring Boot</b>, <b>Hybernate</b>, <b>Golang</b>, <b>Maven</b>, <b>Docker</b>, <b>Github</b>, <b>C++</b>, <b>Python</b>... etc. For more details about my completed projects check out my &nbsp;<a class="text-red" target="_blank" rel="noopener noreferrer" href="https://github.com/florinpop17">Github</a>.
                      <br>
                      <br>
                      See the <a class="text-red" href="/timeline">Timeline</a> for an overview of my progress and accomplishments so far.
                      <br>
                      <br>
                      Feel Free <a class="text-red" href="/contact">Get in touch</a> for any questions you have!!
                  </p>
                </div>
                <div class="col-md-3a col-xs-6a">
                  <div class="service2 text-center">
                      <img src="../assets//img/about/DA.png" alt="">
                      <h6>Data Startcure and Algorithm</h6>
                      <small>What can be more fun than solving algorithm puzzles??</small>
                  </div>
                </div>
                <div class="col-md-3a col-xs-6a">
                    <div class="service2 text-center">
                        <img src="../assets//img/about/operating-system.png" alt="">
                        <h6>Operating System</h6>
                        <small>windows, ios, Android</small>
                    </div>
                </div>
                <div class="col-md-3a col-xs-6a">
                    <div class="service2 text-center">
                        <img src="../assets//img/about/web-development.png" alt="">
                        <h6>Full Stack Development</h6>
                        <small>FrontEnd, Backend, Full-stack</small>
                    </div>
                </div>
                <div class="col-md-3a col-xs-6a">
                    <div class="service2 text-center">
                        <img src="../assets//img/about/database.png" alt="">
                        <h6>Database Engineering</h6>
                        <small>SQL, MySQL, NoSQL</small>
                    </div>
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
