---
layout: post
title: 防止从您的网站发送HTTP Referer标头
date: 2019-09-02
categories: test
tags: HTTP
---

# [防止从您的网站发送HTTP Referer标头](https://geekthis.net/post/hide-http-referer-headers/#exit-page-redirect)

当用户通过链接或HTTP重定向离开您的网站时，用户来自的当前页面的HTTP标头将附加到新请求。在大多数情况下，这不是有害的，但有些情况应该隐藏URL。在本教程中，您将了解一些不同的方法来隐藏或删除请求中的HTTP Referer标头。

请记住，其中一些选项可能并不总是有效。如果浏览器错误地实现了标准，或者用户已禁用特定方法的某些技术，则引用信息将附加到HTTP标头。使用下面标记为“退出页面重定向”的方法，无论禁用哪种技术，以及不支持Referrer策略规范的旧浏览器，都应该有效。

## 使用REL属性

由于HTML5，浏览器都支持的属性更多的选择`rel`的`<a>`标签。根据规范，您可以`rel`通过用空格分隔每个值来提供多个值。其中一个新值是`noreferrer`。此链接类型将阻止浏览器发送当前页面地址。

> 导航到另一个页面时，阻止浏览器通过Referer：HTTP标头发送此页面地址或任何其他值作为referrer。
>
> \- Mozilla

以下是`rel`在链接中使用该属性的示例。它也可以在`<area>`标签上使用，以防止发送引用者信息。

```html
<a href="http://example.com" rel="noreferrer">Example.com</a>
```

## 推荐人政策

第二种方法是使用您网站上的推荐人[政策](https://w3c.github.io/webappsec-referrer-policy/#referrer-policies)。使用此方法，您可以`<meta>`向网站添加标记，也可以向网站`referrerpolicy`上的所有超链接添加属性。截至2017年9月，推荐人政策仍然是工作草案，尚未成为网络标准。最新版本的Microsoft Edge，Firefox，Chrome，Safari，Opera和Android浏览器支持（至少部分支持）使用引荐来源政策。您可以在[“我可以使用推荐人策略”中](http://caniuse.com/#feat=referrer-policy)查看浏览器支持。

要设置您网站上的所有链接以省略推介信息，请将以下`<meta>`标记添加到`<head>`您网站的部分。您可以设置各种值而不是“no-referrer”，可能更好用。当您链接到同一个来源（域）时，“同源”选项将保留引用者数据，但在链接到外部网站或不同子域时省略标题。

```html
<meta name="referrer" content="no-referrer">
```

如果您只希望页面上的一些链接不发送引荐来源数据，则可以基于每个链接指定引用者策略。`<meta>`您只需`referrerpolicy`向要设置自定义策略的每个链接添加新属性，而不是创建标记。

```html
<a href="http://example.com" referrerpolicy="no-referrer">ReferrerPolicy Attribute</a>
```

## 退出页面重定向

唯一应该在没有缺陷的情况下工作的方法是有一个你不介意在`referer`标题内部的退出页面。许多网站都采用这种方法，包括Google和Facebook。如果正确实施，它不会显示引荐来源数据显示私人信息，而只显示用户来自的网站。而不是显示为`http://example.com/user/foobar`新引荐来源数据的引荐来源数据将显示为`http://example.com/exit?url=http%3A%2F%2Fexample.com`。

此方法确实需要额外的编程，但下面的小PHP示例应该有助于您开始使用。该方法的工作方式是让您网站上的所有外部链接转到中间页面，然后重定向到最终页面。下面我们有一个指向网站“example.com”的链接，我们对完整的URL进行URL编码，并将其添加到`url`退出页面的参数中。

```html
<a href="/exit.php?url=http%3A%2F%2Fexample.com">Example.com</a>
```

现在我们在下面有“exit.php”页面代码。我们执行一些URL验证以确保页面被赋予有效的URL以及具有HTTP或HTTPS方案的URL。如果由于某种原因URL无效，我们决定将用户重定向到我们网站的主页，但您可以轻松更改代码以显示错误消息。

```php
<?php
	
	/*
	 * Sets the HTTP headers to redirect the user to a different page
	 * along with settings the HTTP status code to 307 Temporary Redirect
	 */
	function redirect($url) {
		header("Location: {$url}", true, 307);
	}

	/*
	 * Checks if the URL is valid and uses the HTTP or HTTPS scheme.
	 */
	function valid_url($url) {
		if(filter_var($url, FILTER_VALIDATE_URL, FILTER_FLAG_SCHEME_REQUIRED|FILTER_FLAG_HOST_REQUIRED) === false) {
			return false;
		}

		$scheme = parse_url($url, PHP_URL_SCHEME);
		if($scheme !== "http" && $scheme !== "https") {
			return false;
		}

		return true;
	}


	if(!isset($_GET['url'])) {
		// Missing required argument. What should we do?
		redirect("/");
		exit;
	}else{
		$url = $_GET['url'];
		if(valid_url($url)) {
			redirect($url);
			exit;
		}else{
			// Invalid URL. What should we do?
			redirect("/");
			exit;
		}
	}
```

除了直接重定向用户之外，您还可以在“exit.php”页面上显示一个启动画面，其中包含指向最终目的地的链接。这仍将隐藏用户重定向的初始页面，同时向用户发出警告，告知用户他们将离开您的网站。这对于银行和政府网站来说很常见，作为通知访问者他们即将访问不同网站的一种方式。

## 其他方法和信息

还有一些其他方法部分地与一些可能对HTTP Referer头有用的信息一起工作。它们都不是具有足够覆盖率的完整解决方案，可以作为单个解决方案添加。

如果您向网站添加SSL / TLS证书，则`referer`如果用户导航到没有SSL / TLS证书的站点，则不会发送标头。这不是一个完整的解决方案，因为它只适用于没有SSL / TLS证书的网站。您可以通过阅读[RFC 7231的第5.5.2节](https://tools.ietf.org/html/rfc7231#section-5.5.2)了解有关SSL / TLS证书行为方式的更多信息

另一个不太好的选择是在所有超链接上使用JavaScript。然后，您将加载一个新`about:blank`窗口，然后在窗口加载后，您将向新的空白页面添加[元重定向](https://en.wikipedia.org/wiki/Meta_refresh)。这将删除引用者信息，但如果用户禁用了JavaScript，则无法使用。
