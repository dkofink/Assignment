# A1

cat > rdf_template.erb
=HEADER
@prefix : <http://biobeat.org/rdf/ns#> .
=BODY
<%
id = ['chr'+rec.chr,rec.pos,rec.alt].join('_')
%>
:<%= id %>
  :query_id "<%= id %>";
  :chr "<%= rec.chr %>" ;
  :alt "<%= rec.alt.join("") %>" ;
  :pos <%= rec.pos %> ;
  :dp <%= rec.info.dp %>;
  :ref "<%= rec.ref %>" .

cat PIK3CA.vcf |bio-vcf -v --template rdf_template.erb
cat PIK3CA.vcf |bio-vcf -v --template rdf_template.erb > my.rdf
rapper -i turtle my.rdf

rdf=my.rdf
uri=http://localhost:8000/data/http://biobeat.org/data/$rdf
curl -X DELETE $uri
curl -T $rdf -H 'Content-Type: application/x-turtle' $uri

cat > sparql2.rq
PREFIX all:  <http://biobeat.org/rdf/ns#>
SELECT ?id
WHERE
{
  ?id  all:chr  "3".
}

cat sparql2.rq |sparql-query "http://localhost:8000/sparql/" -p
