---
layout: post
title: Languages table (MSSQL)
date: 2009-10-20 12:17
author: ayvazyan
comments: true
categories: [iso, languages, MSSQL, MSSQL]
---
Often I need languages list in database, so I decided to post it here. Hope it will save several minutes for someone ;)
<!--more-->
CREATE TABLE [dbo].[Languages](
	[LanguageId] [char](2) NOT NULL,
	[EnglishName] [varchar](50) NOT NULL,
	[NativeName] [nvarchar](50) NOT NULL,
 CONSTRAINT [PK_Languages] PRIMARY KEY CLUSTERED 
(
	[LanguageId] ASC
)WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

INSERT INTO [Languages] ([LanguageId],[EnglishName],[NativeName]) VALUES 
('ar','Arabic','العربية'),
('bg','Bulgarian','български'),
('ca','Catalan','català'),
('zh','Chinese (Simplified)','中文(简体)'),
('cs','Czech','čeština'),
('da','Danish','dansk'),
('de','German','Deutsch'),
('el','Greek','ελληνικά'),
('en','English','English'),
('es','Spanish','español'),
('fi','Finnish','suomi'),
('fr','French','français'),
('he','Hebrew','עברית'),
('hu','Hungarian','magyar'),
('is','Icelandic','íslenska'),
('it','Italian','italiano'),
('ja','Japanese','日本語'),
('ko','Korean','한국어'),
('nl','Dutch','Nederlands'),
('no','Norwegian','norsk'),
('pl','Polish','polski'),
('pt','Portuguese','Português'),
('ro','Romanian','română'),
('ru','Russian','русский'),
('hr','Croatian','hrvatski'),
('sk','Slovak','slovenčina'),
('sq','Albanian','shqipe'),
('sv','Swedish','svenska'),
('th','Thai','ไทย'),
('tr','Turkish','Türkçe'),
('ur','Urdu','اُردو'),
('id','Indonesian','Bahasa Indonesia'),
('uk','Ukrainian','україньска'),
('be','Belarusian','Беларускі'),
('sl','Slovenian','slovenski'),
('et','Estonian','eesti'),
('lv','Latvian','latviešu'),
('lt','Lithuanian','lietuvių'),
('fa','Persian','فارسى'),
('vi','Vietnamese','Tiếng Việt'),
('hy','Armenian','Հայերեն'),
('az','Azeri','Azərbaycan­ılı'),
('eu','Basque','euskara'),
('mk','Macedonian','македонски јазик'),
('af','Afrikaans','Afrikaans'),
('ka','Georgian','ქართული'),
('fo','Faroese','føroyskt'),
('hi','Hindi','हिंदी'),
('ms','Malay','Bahasa Malaysia'),
('kk','Kazakh','Қазащb'),
('ky','Kyrgyz','Кыргыз'),
('sw','Kiswahili','Kiswahili'),
('uz','Uzbek','U''zbek'),
('tt','Tatar','Татар'),
('pa','Punjabi','ਪੰਜਾਬੀ'),
('gu','Gujarati','ગુજરાતી'),
('ta','Tamil','தமிழ்'),
('te','Telugu','తెలుగు'),
('kn','Kannada','ಕನ್ನಡ'),
('mr','Marathi','मराठी'),
('sa','Sanskrit','संस्कृत'),
('mn','Mongolian','Монгол хэл'),
('gl','Galician','galego'),
('dv','Divehi','ދިވެހިބަސް'),
('sr','Serbian','srpski')
