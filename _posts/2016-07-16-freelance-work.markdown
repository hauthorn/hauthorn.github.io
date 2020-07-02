---
layout: post
title:  "Freelance work"
date:   2016-07-16 12:00:00 +0200
categories: freelance work
excerpt: I've been build business and e-commerce websites for graphical agencies and my own client for 5 years professionally. Here is some of the work, that I'm allowed to disclose.
image: /assets/images/businessparkstruer.jpg
---

I’ve been doing freelance work for my own clients and through a number of advertising and graphical agencies. I started out building simple static sites and dynamic sites in PHP and WordPress. By examining the code of other developers and through a lot of tutorials, books and other material, I started delving into learning object oriented programming and building applications for the desktop. Unfortunately, not a lot of businesses in rural Denmark need anything more than a simple portfolio website or a small e-commerce site.

<div class="mdl-grid">
	<div class="mdl-cell mdl-cell--6-col">
		<img src="/assets/images/businessparkstruer.jpg" alt="BusinessPark Struer site">
		<p class="img-text">The local co-working space BusinessPark Struer</p>
	</div>
	<div class="mdl-cell mdl-cell--6-col">
		<img src="/assets/images/conpleks.jpg" alt="Conpleks site">
		<p class="img-text">Conpleks.com</p>
	</div>
</div>

I therefore started coding and implementing the designs of a web and graphical design business called [Kommuniklame][kommuniklame-site], and other clients soon followed. Before I went on to start [Emplate][emplate-site], I had done more than 200 projects. The projects varied in size from a new image gallery on a portfolio site, to a complete webshops including custom campaign subsites and inventory management and automation.

I discovered the great [Laravel][laravel-site], and also built custom applications for myself and two large clients in the automotive industry and consumer electronics, which I'm not allowed to disclose publicly.

{% highlight php %}
<?php
class Project extends Eloquent
{
	public function timesheets()
	{
		return $this->hasMany('Timesheet', 'project_id');
	}

	public function scopeInvoicable($query)
	{
		return $query->where('status', '=', 2)->orderBy('updated_at', 'DESC');
	}

	public function scopeThisMonth($query)
	{
		$next_month = date('Y-m-d H:i:s', 
			strtotime('first day of next month today'));
		$this_month = date('Y-m-d H:i:s',
			strtotime('first day of this month today'));
		return $query
			->whereBetween('invoicedate', array($this_month, $next_month));
	}
{% endhighlight %}

Some code from a timetracking project for internal use in Laravel 3 (i think). Please note the lovely use of `array()`.

I hope to open-source some of the work I've done in the near future.

[emplate-site]: http://emplate.it
[kommuniklame-site]: http://www.kommuniklame.dk/
[laravel-site]: https://laravel.com/
