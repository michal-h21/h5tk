# h5tk

This module can be used to generate html5 code.
It is very similar to the erector framework
(http://erector.rubyforge.org/).

# Example
## Basic table generation
Just imagine you would want to emit html code
that represents a table. 
With h5tk it's as simple as the following snippet:

	    h5tk.table{
            h5tk.tr{
			h5tk.th{"First"},
			h5tk.th{"Second"},
                h5tk.th{"3"},
                h5tk.th{"4"}
            },
    
            h5tk.tr{
                h5tk.td{"foo1"},
                h5tk.td{"foo2"},
                h5tk.td{"boo3"},
                h5tk.td{"foo4"}
            }
        }

This would genreate the following code:
		
		<table>
			<tr>
				<th> First <th> <th> Second <th> <th> 3 <th> <th> 4 <th>
			</tr>
			<tr>
				<th> foo1 <th> <th> foo2 <th> <th> boo3 <th> <th> foo4 <th>
			</tr>
		</table>

## Full example
For a more complex example, consider this:
	
		local h5tk = require[[h5tk]]

		io.write("<!DOCTYPE html>")
		io.write(h5tk.html{
			h5tk.head{
				h5tk.style{
					"table, th, td { border: 1px solid black; }"
				},
		
				h5tk.title{
					"Geiler ",
					"Titel!!"
				}
			},
			
			h5tk.body{
				h5tk.p{
					style = "bold!"
				},
				
				h5tk.table{
					h5tk.tr{
						(function () 
							local t = {}
							for i=1,2 do
								t[i] = h5tk.th{"foo" .. i}
							end
							return t
						end),
						h5tk.th{"foo"},
						h5tk.th{"boo"}
					},
					
					h5tk.tr{
						h5tk.td{"foo1"},
						h5tk.th{"foo2"},
						h5tk.th{"boo3"},
						h5tk.td{"boo4"}
					}
				}
			}
		})

The code above emits a valid html5 page and _could_ be used
as cgi script for dynamic webcontent. Here is the generated output:

	<!DOCTYPE html>
	<html>
	<head>
	<style>table, th, td { border: 1px solid black; }</style>
	<title>Geiler Titel!!</title>
	</head>
	<body>
	<p style=bold!></p>
	<table>
	<tr>
	<th>foo1</th>
	<th>foo2</th>
	<th>foo</th>
	<th>boo</th>
	</tr>
	<tr>
	<td>foo1</td>
	<td>foo2</th>
	<td>boo3</th>
	<td>boo4</td>
	</tr>
	</table>
	</body>
	</html>
