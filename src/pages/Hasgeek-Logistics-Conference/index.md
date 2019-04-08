---
title: [Hasgeek Logistics Conference] Go JEK : Automated Daily Run Sheet
date: "2018-11-25"
---

Automating the Daily Run sheet challenges and solutions. 
<!-- end -->

    * The DRS creation is almost always manual. 
    * Source of data : customer address
        *  Structure the address : 
            * Format changes across the state.
            * Also the problem can be more complicated when 3rd party collect data
            * Make a text corpus.
            * Problems : Spelling mistakes, Combined text, Separator,  Gibberish Text, No address Information
        * Named Entity Recognition
            * Ground Truth : Dispatch Centre lat long, and find the complete address with google which is mostly formatted, comma separated address. 
            * Get a vocabulary of different classes - roads, apartment, etc
            * Create a spell checker [old address? ]
                * Develop a similarity score where you compare and replace. 
            * Preprocess the data:
                * Remove all the English stop words and the address stop words. 
            * Supervised Training Data Set
                * Create custom address tags
                * FNS FNC FNC : manual ways in which addresses are written. 
                * Training the data around ~8.5 K address. 
            * Model Building
                * Maximum Entropy Model
                    * Model will predict tag for a given token
                    * Feature set to be generated maxent based on business case [ eg: when the 3rd word is Apartment then the tag is BNC]
                    * These features goes to MaxEnt ~98% tags of the words
                * Geo Coding
                    * Get a tags for all the addresses
                    * From a priority of the address tags, not all are important
                    * Definite LMI >>> Importance of non definitive LMI
                    * Final accuracy should be sensible ~200m 
        * Cluster
            * Modified K-Means cluster. 
            * Business decisions:
                * One cluster cannot be 35 and other 85, the k can be defined beforehand. 
    * Questions: 
        * Google needs a structured address, if it cannot be identified by google then it just returns the lat long of the recognised centroid. 
        * Taking the feedback and feeding it into the systems
        * Why not a vehicle routing problem over a cluster? FE generally knows the area. 
        * Clustering need to modified for the time slots: sub cluster
