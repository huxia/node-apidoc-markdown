# <%= project.name %> (<%= project.version %>)

<% if (project.description){ %><%= project.description.replace(/<\/(ul|ol)>/g, '\n</$1>').replace(/<\/\w+>\s*<p>/g, '\n').replace(/<li>/g, '\n* ').replace(/<[^>]+>/g, '') %><% } //if description %>

## 菜单

<% Object.keys(data).forEach(function (group) { -%>
- [<%= group %>](#<%=: group | mlink %>)
	<% Object.keys(data[group]).forEach(function (sub) { -%>
- [<%= data[group][sub][0].title %>](#<%=: data[group][sub][0].type | mlink %>-<%=: data[group][sub][0].url | mlink %>) `<%-: data[group][sub][0].type | upcase %> <%= data[group][sub][0].url %>`
	<% }); -%>

<% }); %>

<% if (prepend) { -%>
<%- prepend %>
<% } -%>
<% Object.keys(data).forEach(function (group) { -%>
# <%= group %>

<% Object.keys(data[group]).forEach(function (sub) { -%>
## <a name="<%=: data[group][sub][0].type | mlink %>-<%=: data[group][sub][0].url | mlink %>"></a><%= data[group][sub][0].title %>

	<%-: data[group][sub][0].type | upcase %> <%= data[group][sub][0].url %>

<% if (data[group][sub][0].header && data[group][sub][0].header.fields.Header.length) { -%>
### Headers

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
<% data[group][sub][0].header.fields.Header.forEach(function (header) { -%>
| <%- header.field %>			| <%- header.type %>			| <%- header.optional ? '**optional**' : '' %> <%- header.description.replace(/<[^>]+>/g, '') %>							|
<% }); //forech parameter -%>
<% } //if parameters -%>
<% if (data[group][sub][0].parameter && data[group][sub][0].parameter.fields.Parameter.length) { -%>

### 参数

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
<% data[group][sub][0].parameter.fields.Parameter.forEach(function (param) { -%>
| <%- param.field %>			| <%- param.type %>			| <%- param.optional ? '**optional**' : '' %> <%- param.description.replace(/<[^>]+>/g, '') %>							|
<% }); //forech parameter -%>
<% } //if parameters -%>
<% if (data[group][sub][0].description){ -%>

### 说明

<%= data[group][sub][0].description.replace(/<\/(ul|ol)>/g, '\n</$1>').replace(/<\/\w+>\s*<p>/g, '\n').replace(/<li>/g, '\n* ').replace(/<(\/?code)>/g, '`').replace(/<[^>]+>/g, '') %>
<% } //if description %>
<% if (data[group][sub][0].examples && data[group][sub][0].examples.length) { -%>

### 🌰

<% data[group][sub][0].examples.forEach(function (example) { -%>
<%= example.title %>

```
<%- example.content %>
```
<% }); //foreach example -%>
<% } //if example -%>

<% if (data[group][sub][0].success && data[group][sub][0].success.examples && data[group][sub][0].success.examples.length) { -%>
### 输出格式

<% data[group][sub][0].success.examples.forEach(function (example) { -%>
<%= example.title %>

```
<%- example.content %>
```
<% }); //foreach success example -%>
<% } //if examples -%>
<% if (data[group][sub][0].error && data[group][sub][0].error.examples && data[group][sub][0].error.examples.length) { -%>
### 错误格式

<% data[group][sub][0].error.examples.forEach(function (example) { -%>
<%= example.title %>

```
<%- example.content %>
```
<% }); //foreach error example -%>
<% } //if examples -%>
<% }); //foreach sub  -%>
<% }); //foreach group -%>

