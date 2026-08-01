# Block-meta-training-into-WooCommerce-High-CPU-usage-
these two simple sets block meta training bots, my specific issue was monitoring WooCommerce

#Place this into your nginx directives:
if ($http_user_agent ~* "meta-externalagent|FacebookBot|facebookexternalhit") { return 403; }
if ($args ~ "add-to-cart=") { set $bot_cart "A"; }
if ($http_user_agent ~* "bot|crawler|spider|slurp") { set $bot_cart "${bot_cart}B"; }
if ($bot_cart = "AB") { return 403; }


#Place this into your robots.txt:
Disallow: /*add-to-cart=
Disallow: /cart/
Disallow: /checkout/
Disallow: /my-account/
#and append at the end:
User-agent: meta-externalagent
Disallow: /

User-agent: GPTBot
Disallow: /

User-agent: ClaudeBot
Disallow: /

User-agent: CCBot
Disallow: /
