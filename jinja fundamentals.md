Control Statements:
allt som har {% då vet man direkt att det är control statements.

{% set variable_a = 10 %}
{% if name == "Bard": % } .... {% endif %}
{% for i in range(variable_a) %} ... {% endfor % }
The content of control statments are not printed in the final generated code.

Expressions:
{{ 10 + 20 }
{{variable_a}
These are printed in the final version of the code

Texts:
SELECT UNION, texts are not evaluated just printed in the final code

comments:
{#  this is a comment #}



{# This jinja code generates select statements to print numbers from 0 to 9 #}
{% set max_number = 10 %}
{% for i in range(max_number) %}
    Select {{ i }} AS number
    {% if not loop.last %}
	UNION
    {% endif %}
{% endfor %}




