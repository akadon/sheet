software prozesse:
waterfall : [requirement / design / integrartion / QA(verification) / installation(deployment) / maintanace] -> product
agile : [waterfall] -> feature 
scrum : sprint planen / daily meeting / review  | backlogs : [owner -> anforderung product ,dev -> sprint, master -> prozess review]
kanban : [board -> visualiziert] : backlog | todo | in progress | testing | done

Linux:
/etc/ssh/ssh_config
/etc/haproxy/haproxy.cfg
/etc/nginx/nginx.conf

git:
	git config --global user.name "akadon"
	git config --global user.email "email"
	gpg --gen-key
	gpg --list-secret-keys --keyid-format=long
      gpg --armor --export FD8EA2EED73EFE92
	git config --global user.signingkey FD8EA2EED73EFE92
	git config --global commit.gpgsign true

ca keys:
	openssl genrsa -out rootCA.key 4096 #root key
	openssl genrsa -out local.key 4096 #local key
	openssl req -new -key local.key  -extensions req_ext -out local.crt -config local.conf -out local.csr # csr
	openssl req -x509 -key local.key -sha256 -nodes -days 365 -subj "/CN=local.crt"  -extensions req_ext -out local.crt -config local.conf # crt
	openssl req -x509 -sha256 -new -nodes -key rootCA.key -days 365 -subj "/CN=rootCA.crt"  -extensions req_ext -out rootCA.crt -config root.conf # root crt
	openssl req -x509 -in local.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out local.crt -days 365 -sha256 -extfile root.conf -extensions req_ext

ssh:
	ssh-keygen -t rsa -b 4096 -C "email" -f $HOME/.ssh/id_rsa -q -N ""
	ssh-keygen -t ed25519  -C "email" -f $HOME/.ssh/id_rsa  -q -N ""
	cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

varriablen: String s = “string”;char c = ‘c’;
if: if (true) {...} else if (true) {...} 
for: for (int i =0; i <=len; i++) {...}
while: while (true) {...}
exception: try {...} catch (Exception e) {...} catch {...} finally {...}
classes: Class MyClass{ /*Class definition*/} { MyClass ClassObj = new MyClass(); }
Method: static void MyMethod(){} {MyMethod();} 

react: https://reactjs.org/docs/hooks-intro.html
	import { useState } from 'react';
	export const Counter = ({ lines = 10 }) => { 
		const [count, setCount] = useState(0); 
		const addup = () => { setCount(count => count + 1)}; 
		return (<div>{count}<br></br><input type="submit" onClick={addup}></input></div>) 
	};
	
	export function useCounter() {
	  const [value, setValue] = useState(0);
	  const [isEven, setIsEven] = useState(false);
	  
	  useEffect(() => {
		if (value % 2 === 0) {
		  setIsEven(true);
		} else {
		  setIsEven(false);
		}
	  }, [value]);

	  const handleIncrement = () => {
		setValue(value + 1);
	  };
	  const handleDecrement = () => {
		setValue(value - 1);
	  };

	  return [value, isEven, handleIncrement, handleDecrement];
	}
	
	const [ value, isEven, handleIncrement, handleDecrement ]= useCounter();

javascript:
	import Head from 'next/head'   export default Home
	async function logJSONData() {const response = await fetch("http://example.com/movies.json",{headers: {'Accept': 'application/json','Content-Type': 'application/json'},method: "POST",body: JSON.stringify({a: 1, b: 2})}).json();}
	const elem = document.getElementById("");

php:
	function foo(int $a, int $b) { $array = [1, 2, 3]; }
	$pdo = new PDO('mysql:host=localhost;dbname=databasename', 'username', 'password');
	$sql = "SELECT * FROM users"; foreach ($pdo->query($sql) as $row) {echo $row['email']."<br />";}

html:
	<form action="/action_page.php" method="post">
  		<label for="fname">First name:</label>
  		<select name="gender"><option selected="selected" value="male">Male</option></select>
  		<textarea cols="20" name="comments" rows="5">Comment</textarea>
  		<input type="submit" value="Submit" onclick="myFunction()">
	</form> 
	<table>
 		<caption>x</caption>
 		<thead>
   			<tr>
				<th>x</th>
   			</tr>
 		</thead>
 		<tbody></tbody>
 		<tfoot> </tfoot>
	</table>
	<ul><li>First</li></ul>
	<img src="/demo.jpg" alt="description" height="48" width="100">

css: 
	https://htmlcheatsheet.com/css/
	.container {
   		display: flex;
		flex-wrap: nowrap | wrap | wrap-reverse;
   		flex-direction: row | row-reverse | column | column-reverse; /* optional */
   		justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right; /* optional */
   		flex-direction: row | column; /* optional */
	}

	.image-gallery {
  		display: grid;
  		grid-template-columns: 1fr 2fr;
  		grid-template-rows: repeat(2, 2fr 1fr);
 		grid-gap: 20px;
	}

bootstrap (classes):
	Layout: (grid) container-sm -> row -> col-sm-6
	Layout: (flex) d-flex flex-row -> p-2
	button: btn btn-primary
	card: card ->  card-body -> card-title | card-text | card-link
	form: form-group -> form-control | form-text
	nav: nav -> nav-item -> nav-link
	img: img-fluid
	links: link-primary

tailwind:	
	Layout: (grid) grid grid-cols-4 gap-4	
	Layout: (flex) flex -> flex-initial w-64 | flex-1 w-64 | flex-auto
	button: btn 
	card: max-w-sm bg-white border border-gray-200
	form: block text-sm font-medium
	img: h-auto max-w-full
	links: font-medium text-blue-600 dark:text-blue-500 hover:underline

blade:
    {{ $var }} - Echo content
    {{ $var or 'default' }} - Echo content with a default value
    {{{ $var }}} - Echo escaped content
    {{-- Comment --}} - A Blade comment
    @extends('layout') - Extends a template with a layout
    @if(condition) - Starts an if block
    @else - Starts an else block
    @elseif(condition) - Start a elseif block
    @endif - Ends a if block
    @foreach($list as $key => $val) - Starts a foreach block
    @endforeach - Ends a foreach block
    @for($i = 0; $i < 10; $i++) - Starts a for block
    @endfor - Ends a for block
    @while(condition) - Starts a while block
    @endwhile - Ends a while block
    @unless(condition) - Starts an unless block
    @endunless - Ends an unless block
    @include(file) - Includes another template
    @include(file, ['var' => $val,...]) - Includes a template, passing new variables.
    @each('file',$list,'item') - Renders a template on a collection
    @each('file',$list,'item','empty') - Renders a template on a collection or a different template if collection is empty.
    @yield('section') - Yields content of a section.
    @show - Ends section and yields its content
    @lang('message') - Outputs message from translation table
    @choice('message', $count) - Outputs message with language pluralization
    @section('name') - Starts a section
    @stop - Ends section
    @endsection - Ends section
    @append - Ends section and appends it to existing of section of same name
    @overwrite - Ends section, overwriting previous section of same name
    @Isset($records) // $records is defined and is not null...
    @endisset
    @production //code to be displayed just when .env is set to production
    @endproduction
    @auth //code for logged-in users
    @endauth
    @guest //code for guest users
    @endguest

wordpress:
	https://websitesetup.org/wp-content/uploads/2020/04/WordPress-Cheat-Sheet-Summary.png
	get_sidebar()
	<?php if(have_posts()): ?>
	<?php while(have_posts()): the_post();?>
	<?php the_title();the_content();the_tags();the_category(); ?>
	<?php endwhile; ?>
	
cli:
	laravel: https://learninglaravel.net/cheatsheet/
		 php artisan make:policy PostPolicy
		 php artisan tinker 
		 php artisan up 
		 php artisan optimize
		 php artisan serve 
		 php artisan migrate
	c#: 
		add-migration "name"
		update-database

regex:
	i perform case-insensitive matching
	g perform a global match
	m perform multiline matching
	\ Escape character
	\d find a digit
	\s find a whitespace character
	\b find match at beginning or end of a word
	n+ contains at least one n
	n* contains zero or more occurrences of n
	n? contains zero or one occurrences of n
	^ Start of string
	$ End of string
	\uxxxx find the Unicode character
	. Any single character
	(a|b) a or b
	(...) Group section
	[abc] In range (a, b or c)
	[0-9] any of the digits between the brackets
	[^abc] Not in range
	a{2} Exactly 2 of a
	a{2,} 2 or more of a
	a{,5} Up to 5 of a
	a{2,5} 2 to 5 of a
	a{2,5}? 2 to 5 of a, ungreedy
	[:punct:] Any punctu­ation symbol
	[:space:] Any space character
	[:blank:] Space or tab




