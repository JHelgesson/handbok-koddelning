# Handbok för koddelning

## Författare

- Dennis Lundberg, Mälardalens högskola
- Dennis Sjögren, Högskolan Dalarna
- Karl Hermansson, Linnéuniversitetet
- Oscar Celsing, Blekinge Tekniska Högskola
- Patric Jansson, Kungliga Tekniska högskolan
- Erik Skaffman, Kungliga Musikhögskolan
- Per Hörnblad, Umeå universitet

## Överenskommelser

### Licens

Oavsett om källkoden kommer att vara öppet tillgänglig för alla eller begränsad
till några få så är det bra om den har en licens. Licensen reglerar vad en
person som har tillgång till källkoden får göra med den. Det finns exempel på
myndigheter som tagit policybeslut kring öppen källkod, t.ex. Myndigheten för
digital förvaltning [[1]].

#### Rekommendationer

För öppen källkod rekommenderar vi att man använder sig av MIT-licensen [[2]] då
den är enkel och välkänd.

### Åtaganden och utfästelser

Vilket ansvar har man när man publicerar eller konsumerar källkod? För att
förstå det behöver man veta under vilka förutsättningar som en kodbas är delad.
Det finns några parametrar som kan användas för att beskriva detta.

#### Utvecklingsprocess

En parameter är hur mogen utvecklingsprocessen är. Det finns en internationellt
erkänd modell som heter Capability Maturity Model [[3]], som i 5 nivåer mäter
mognadsgraden. Den här ger en inblick i hur mogen processen för utvecklingen av
kodbasen är.

#### Mognad

Mognad beskriver hur välanvänd och vältestad en kodbas är. Vi har inte hittat
någon etablerad standard, utan har tagit fram en egen. Vår föreslagna skala
definierar 5 nivåer av mognad:

1. Omogen - vi vet inte om koden funkar, använd den på egen risk
2. Har fungerat - vi har använt koden tidigare och då fungerade den
3. Används - vi använder koden i produktion och tror att den gör det den ska,
   men vi har inga tester som säkerställer det
4. Testad - vi använder koden i produktion, och automatiska tester säkerställer
   en del av funktionaliteten
5. Mogen – vi använder koden i produktion utan problem, och automatiska tester
   säkerställer stora delar av funktionaliteten

#### Förvaltning

Förvaltning beskriver hur man tar hand om kodbasen och hur man hanterar
förändringar. Inte heller här har vi hittat någon etablerad standard för att
mäta detta, så vi har tagit fram en egen. Vår skala definierar 5 nivåer av
förvaltning:

1. Ingen - vi har inte rört koden på länge och det finns ingen kunskap kvar om
   hur den fungerar
2. Minimal - om det dyker upp kritiska fel, t.ex. säkerhetshål, så går vi in och
   rättar till dem, men i övrigt görs inga förändringar längre
3. Ad hoc - om det finns behov av att genomföra förändringar så görs det av
   någon individ på eget initiativ
4. Förvaltad - det finns en utsedd individ eller grupp som ansvarar för vilka
   förändringar som ska genomföras och i vilken ordning
5. Aktivt förvaltad – den utsedda förvaltningsgruppen träffas regelbundet, går
   igenom inkomna ändringsbegäran och beslutar om vilka förändringar som ska
   genomföras i den närmaste framtiden.

#### Rekommendationer

En kodbas som delas bör dokumentera vilken nivå som kodbasen ligger på, för var
och en av dessa parametrar.

## Källkod

### Repositories för källkod

Det kan finnas kodbaser som antingen är öppen källkod (open source [[4]]) eller
sluten källkod (closed source [[5]]). Dessa kodbaser kan i sin tur finnas i
källkodsrepositories som är öppna för alla eller begränsade till några få.

Det bör finnas en dokumentation för ett källkodsrepo, där det åtminstone ska
finns en readme med en kort beskrivning, kontaktpersoner, vilken licens som
används samt vilket år som kodbasen påbörjades. Det är bra om man har frågor om
en viss kodbas. Det blir ännu bättre om man lägger till de självskattningar som
återfinns i kapitlet om åtaganden och utfästelser. Det skulle kunna se ut så
här:

> Beskrivning: en tjänst som håller information om schemalagda driftavbrott  
> Lärosäte: Mälardalens högskola  
> Kontaktperson: Dennis Lundberg  
> Licens: MIT  
> Påbörjades: 2017  
> Utvecklingsprocess: 3 Defined  
> Mognad: 4 Testad  
> Förvaltning: 3 Ad hoc  

Det kan finnas behov av dual-home för vissa repositories. Det skulle t.ex. kunna
vara ett internt lokalt repo för utveckling (t.ex. Git i TFS) och ett publikt
repo (t.ex. GitHub) för releaser. Anledningen till detta kan vara av tekniska
skäl, t.ex. att man inte har tillräckligt med licenser för det lokala repot för
att kunna släppa in externa utvecklare, eller att man är rädd att checka in
hemligheter i ett publikt repo.

Bland de lärosäten som författarna tillhör används bland annat GitHub Enterprise
on-prem, open source-repositories på GitHub, privata repositories på GitHub,
Azure DevOps, Git i TFS och Apache Subversion.

#### Rekommendationer

Utvecklingsbranschen har under senare år gått över mer och mer till distribuerad
versionshantering [[6]], där Git är det system som har fått störst genomslag. Om
man letar efter ett repository för källkod idag rekommenderar vi att man väljer
Git i någon form.

Det finns olika sätt som man kan använda sig av Git, antingen som en extern
tjänst som t.ex. GitHub [[7]], GitLab [[8]], Bitbucket [[9]],
Azure DevOps [[10]] eller som en lokal installation. Vilket man väljer här beror
på vad lärosätet har för strategi för att använda externa tjänster och vilken
kostnad man är beredd att ta. Det finns både alternativ som är gratis och som
man får betala för.

### Strategi för branch och merge

Det är viktigt att ha en tydlighet när det gäller branching [[11]] samt hur och
när man gör en merge. Därför bör man välja en branchingstrategi [[12]] för varje
kodbas. För de lärosäten som författarna tillhör så används huvudsakligen
strategierna ”no branching” och ”feature branching”.

### Behörighet

Vem får göra vad och när? Ett samarbete runt en kodbas börjar troligtvis med att
ett lärosäte använder kod som ett annat lärosäte har skrivit. Med tiden lär man
sig koden och börjar komma med patchar och förslag på ny funktionalitet. Det kan
på längre sikt innebära att båda lärosätena utvecklar koden. Det finns exempel
inom sektorn där detta har varit fallet. Då behöver man fundera på vem ska få
rättigheter att modifiera koden. Man kan ge behörighet till ett privat
källkodsrepository genom att lägga till enskilda personer, eller så kan man be
folk att skicka in pull requests eller motsvarande med önskade förändringar.

### Kodkvalitet

Det finns olika sätt att mäta kodkvalitet, och ju fler av dessa som en kodbas
har mätts efter desto enklare är det för någon att avgöra om just den här
kodbasen är något för dem.

Automatiska tester brukar delas in i enhetstester [[13]] och
integrationstester [[14]]. De är tester av koden som körs automatiskt av verktyg
i samband med att kodbasen byggs eller kompileras. Under dessa tester så körs
delar av kodbasen och dess resultat utvärderas. Om några tester misslyckas kan
bygget avbrytas och vägra gå igenom förrän testerna har lagats. Den typen av
tester ger programmerarna ett större självförtroende att göra förändringar av
kodbasen.

Vid statisk kodanalys [[15]] används verktyg som analyserar koden och tittar
efter vanliga typer av programmeringsfel. Det här kan hjälpa till att hitta
potentiella buggar i kodbasen.

För en kodbas som ligger på GitHub kan man säkerställa kvaliteten på en
pull request [[16]] genom att lägga till en koppling till Travis [[17]], som
gör att alla pull requests automatiskt byggs och kodbasens tester körs. Om
testerna vid ett sådant bygge misslyckas, kan man skicka tillbaka bollen till
den som skapade pull requesten och be dem laga sina förändringar och göra en ny
pull request. Det är dock inte säkert att alla kodbaser har automatiska tester.

#### Rekommendationer

Det är bra om varje kodbas dokumenterar på vilka sätt man mäter kodkvalitet.

### Hur vi skriver kod

Kod ska vara skriven med ett mindset att koden ska kunna förstås, användas och
förvaltas av personer på andra lärosäten, eller av kollegorna inom det egna
lärosätet för den delen.

Kod bör vara så pass allmängiltig att den kan användas av vilket annat lärosäte
som helst, utan att behöva förändra koden. Om det finns behov av att göra
anpassningar så kan det göras på olika sätt:

- Konfiguration, används oftast när det är få och mindre delar som skiljer
  mellan lärosäten, t.ex. hur datum ska formateras.
- Feature toggles, som innebär att man kan stänga av eller slå på hela
  funktioner.
- Använd ett API för de delar som skiljer sig mellan lärosäten. Sedan kan varje
  lärosäte ha en egen implementation för sin logik.

## Ärende- och förändringshantering

En del av förvaltningen av en kodbas handlar om att genomföra förändringar. Här
är det till stor hjälp om man kan ha något systemstöd för det. Vilken nivå av
systemstöd som en kodbas behöver beror bland annat på hur förvaltningen ser ut,
men även på kodbasens storlek. Generellt kan man säga att ju större kodbasen är
och ju mer förvaltad kodbasen är desto större behov av systemstöd har man.

För stora kodbaser eller där verksamheten är involverad i arbetet med
förändringshantering kan ett renodlat ärendehanteringssystem för
mjukvaruutveckling, som t.ex. Atlassian JIRA Software [[18]], vara ett
alternativ.

För en mindre kodbas som ligger på GitHub kan man använda GitHub issues [[19]]
i kombination med pull requests för förändringsförslag. Ett annat system för att
hantera ärenden i mindre skala är Trello [[20]], även om det inte är utformat
specifikt för mjukvaruutveckling.

Det är till slut kodbasens ägare som behöver välja hur ärenden ska hanteras.

### Rekommendationer

Om en kodbas ska delas mellan flera lärosäten så bör hanteringen av ärenden och
förändringar ske på ett sätt så att även personer från andra lärosäten än det
som skapat kodbasen kan delta i det arbetet. Vi rekommenderar att använda något
webbaserat systemstöd för ärendehantering.

## Versionsnumrering

Det finns många olika sätt att använda versionsnummer, där vissa är mer vanliga
bland vissa programmeringsspråk. På senare tid har ett initiativ som kallas
SemVer [[21]] dykt upp, som ett försök att samordna regler och krav på
versionsnummer. Det är idag vanligt att en kodbas har beroenden till många andra
kodbaser, för att hantera vissa delar av systemet. För kodbaser som används av
andra kodbaser på detta sätt är det extra viktigt med en tydlig strategi för
versionsnummer och att man håller sig till den.

I korthet pratar man om att ett versionsnummer består av minst tre delar: major,
minor och patch. Beroende på vilken typ av förändring man har gjort så finns det
regler för vad nästa versionsnummer ska vara. Om man t.ex. gör ändringar av
koden som inte är bakåtkompatibla, blir det en ny major-version.

Här är det viktigt att tänka på andra utvecklare än sig själv. När det är dags
att avgöra vad nästa versionsnummer ska vara behöver du ställa dig frågan: hur
påverkar den förändring jag har gjort andra utvecklare eller lärosäten? För
libraries som används av 10000-tals andra, som t.ex. libraries från
Apache Commons, kan ett felaktigt satt versionsnummer få stora negativa
konsekvenser.

### Rekommendationer

Vi rekommenderar att man alltid använder sig av SemVer för versionsnumrering.

## Konfiguration

Det finns många olika metoder för att lösa konfiguration, men det viktigaste att
tänka på är att faktiskt ha möjligheten att konfigurera överhuvudtaget. Om ett
annat lärosäte ska kunna använda en kodbas så är det vanligt att de vill justera
beteendet på något vis. Här gäller det att som utvecklare tänka till och försöka
förutse vilka saker som behöver vara konfigurerbara. Med tiden lär man sig det
här och då krävs det inte någon extra insats.

Exempel på saker som kan behöva konfigureras är:

- URL till en server som koden behöver prata med
- sökvägen till en fil som ska läsas eller skrivas
- hur loggningen ska gå till
- användarid och lösenord till en databas som anropas

Det finns en uppsjö av olika alternativ för att lagra konfigurationen för en
kodbas. Vilket man väljer beror på storleken på kodbasen, hur mycket det är som
ska konfigureras och vem som ska kunna förändra konfigurationen. Några exempel
är properties-filer (key-value pairs), xml-filer eller miljövariabler.

Det finns även API:er för konfiguration. Ett exempel på det för Java är
Commons Configuration [[22]]. Det abstraherar läsning och skrivning av
konfiguration, så att koden ser nästan likadan ut oavsett om konfigurationen
lagras i xml-filer eller i en databas. Det ger en flexibilitet för konsumenten
av kodbasen att välja ett sätt för konfiguration som passar dem. 

### Rekommendationer

Tänk noga igenom vilka delar av kodbasen som kan behöva konfigureras och se till
att konfigurationen är flexibel. Om en kodbas använder ett API för konfiguration
så är det en bonus, men absolut inget krav.

## Loggning

Loggning är något som är väldigt viktigt för konsumenten av en kodbas. Det är
därför av största vikt att konsumenten har en möjlighet att styra hur loggningen
går till. För att lösa det finns det som vi ser det två alternativ.

### Använd ett API för loggning

Genom att använda ett API för loggning i sin kod så kan man överlåta till
konsumenten att välja en implementation för loggning som passar just dem. Vilket
API man ska använda varierar mellan olika programmeringsspråk. Här kommer några
exempel:

- Java
  - Apache Commons Logging [[23]]
  - Apache Log4J [[24]]
  - Java Util Logging [[25]]
  - SLF4J API [[26]]
- .NET
  - Apache Log4Net [[27]]
  - NLog [[28]]
  - Serilog [[29]]
  - .NET Core Logging [[30]]

Om ett lärosäte använder både Java och .NET kan det vara en idé att använda
Log4J för Java och Log4Net för .NET, då de är systerprojekt som har liknande
konfiguration och utmatningsmöjligheter.

### Se loggning som en ström av händelser

The Twelve-Factor app [[31]] ser på loggar som en ström av händelser som skickas
till stdout. Det är sedan upp till konsumenten att fånga denna ström av
händelser och skicka dem dit den vill.

### Rekommendationer

Använd ett loggnings-API i din kodbas, speciellt om det är ett library eller
motsvarande. Det gör att konsumenten av din kodbas själv kan välja en
loggningsimplementation som passar dem. Även om du har en
slutanvändarapplikation är det best practice att använda ett API för loggning.

## Releaser

Det är viktigt att ha reproducerbara byggen för releaser. Det innebär att man
oavsett när i tiden man bygger en release av en produkt ska det artefakt som
kommer ut i andra änden se likadant ut. För att säkerställa detta bör man
automatisera sin releaseprocess. Under ett bygge av en release ska de
automatiska tester som finns köras, för att säkerställa kvaliteten på releasen.

Det är en stor fördel att använda sig av någon plattform för att få hjälp att
automatisera sina releaser. Några spelare inom detta område är:

- Azure DevOps [[32]]
- Jenkins [[33]]

### Rekommendationer

Se till att automatisera er releaseprocess. Hur ni gör det spelar mindre roll,
det viktiga är att releaser görs automatiskt.

## Repositories för binärer/paket 

Det finns fördelar med att använda repositories för binärer/paket [[34]] . Dessa
kan vara öppna eller slutna. För öppen källkod är det bäst att använda de
standarder som är etablerade för respektive utvecklingsplattform

- Java - Maven central [[35]]
- .NET - NuGet [[36]]
- Node.js - npm [[37]]
- Python - Python Package Index [[38]]

Om man har sluten källkod och vill ha ett eget repository för binärer/paket så
finns det flera alternativ att välja mellan. En del är gratis och en del kostar
pengar. De som listas nedan har stöd för alla plattformarna som listades ovan
och fler därtill.

- JFrog Artifactory [[39]]
- Sonatype Nexus Repository OSS [[40]]
- Sonatype Nexus Repository Pro [[41]]

Finns det förutsättningar att skapa ett lärosätesneutralt repository för lagring
av binärer och paket för delad kod?

### Rekommendationer

Det finns inget krav på att delad kod ska finnas tillgänglig i ett binärt
repository, men det är en bonus om det gör det. Så länge källkoden är
tillgänglig och byggprocessen är deterministisk kan man alltid producera en egen
binär.

## Informationsspridning

Ett problem är hur vi ska kunna sprida kunskap inom sektorn om vilken kod som
faktiskt är delad. Vi behöver nog sammanställa en katalog över detta på något
sätt. Det är något som behöver lösas på sikt.

<!-- Referenser -->

[1]: https://www.digg.se/nyheter--publikationer/nyheter/digg-tar-policybeslut-kring-oppen-kallkod
[2]: https://opensource.org/licenses/MIT
[3]: https://sv.wikipedia.org/wiki/Capability_Maturity_Model
[4]: https://opensource.org/osd
[5]: https://en.wikipedia.org/wiki/Proprietary_software
[6]: https://en.wikipedia.org/wiki/Distributed_version_control
[7]: https://github.com/
[8]: https://about.gitlab.com/
[9]: https://bitbucket.org/product/
[10]: https://docs.microsoft.com/en-us/azure/devops/user-guide/source-control
[11]: https://en.wikipedia.org/wiki/Branching_(version_control)
[12]: https://www.agileconnection.com/article/picking-right-branch-merge-strategy
[13]: https://en.wikipedia.org/wiki/Unit_testing
[14]: https://en.wikipedia.org/wiki/Integration_testing
[15]: https://en.wikipedia.org/wiki/Static_program_analysis
[16]: https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests
[17]: https://en.wikipedia.org/wiki/Travis_CI
[18]: https://en.wikipedia.org/wiki/Jira_(software)
[19]: https://help.github.com/en/github/managing-your-work-on-github/about-issues
[20]: https://trello.com/sv
[21]: https://semver.org/
[22]: https://commons.apache.org/proper/commons-configuration/
[23]: https://commons.apache.org/proper/commons-logging/
[24]: https://logging.apache.org/log4j/2.x/
[25]: https://docs.oracle.com/javase/8/docs/api/java/util/logging/package-summary.html#package.description
[26]: http://www.slf4j.org/
[27]: https://logging.apache.org/log4net/
[28]: https://nlog-project.org/
[29]: https://serilog.net/
[30]: https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging/
[31]: https://12factor.net/
[32]: https://azure.microsoft.com/en-us/services/devops
[33]: https://jenkins.io/
[34]: https://en.wikipedia.org/wiki/Software_repository
[35]: https://maven.apache.org/repository/
[36]: https://www.nuget.org/
[37]: https://en.wikipedia.org/wiki/Npm_(software)
[38]: https://pypi.org/
[39]: https://jfrog.com/artifactory/
[40]: https://www.sonatype.com/nexus-repository-oss
[41]: https://www.sonatype.com/product-nexus-repository
 