<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8" >
    <title>Empirical Evaluation of: A Calculus for Modular Loop Acceleration (and Non-Termination Proofs)</title>
    <style>
      table, th, td {border: 1px solid black;}
      td {text-align: center}
    </style>
  </head>
  <body>

    <p>
      This is the empirical evaluation of the papers <a href="index.html#accel"><i>A Calculus for Modular Loop Acceleration</i></a> and <a href="index.html#nonterm"><i>A Calculus for Modular Loop Acceleration and Non-Termination Proofs</i></a>.
      You can find the source code for our tool LoAT at <a href="https://github.com/aprove-developers/LoAT">GitHub</a>.
    </p>

    <p>Moreover, we refer to the <a href="https://aprove-developers.github.io/LoAT/">general LoAT website</a> for further information.</p>

    <h1 id="accel"><a href="https://arxiv.org/abs/2001.01516">A Calculus for Modular Loop Acceleration</a></h1>

    <h2>Artifact Evaluation</h2>

    <a href="https://doi.org/10.5281/zenodo.3676348">Here</a> you can find the zip-file for the artifact evaluation committee.

    <h2>Downloading LoAT</h2>

    <p>
      We provide a
      <a href="https://github.com/aprove-developers/LoAT/releases/tag/tacas20">pre-compiled binary of LoAT (Linux, 64 bit)</a>.
      Apart from that, LoAT is open-source and the source code of the version that was used for our evaluation is available on <a href="https://github.com/aprove-developers/LoAT/tree/tacas20">Github</a>.
    </p>

    <h2>Examples</h2>

    <ul>
      <li><a href="loops.zip">Here</a> you can find the loops that we used for our evaluation.</li>
      <li><a href="flata.zip">Here</a> you can find the loops that we used for our evaluation in Flata's input format.</li>
      <li><a href="examples.zip">Here</a> you can find the examples from our paper.</li>
    </ul>

    <h2>Evaluation</h2>

    <h3>StarExec-Jobs</h3>

    <p>
      Below we provide links to the StarExec-Jobs of our evaluation.
    </p>
    <ul>
      <li><a href="https://www.starexec.org/starexec/secure/details/job.jsp?id=37260">full version</a> of our acceleration calculus
        <ul><li>Invocation: <code>loat-static $INPUT</code></li></ul></li>
      <li><a href="https://www.starexec.org/starexec/secure/details/job.jsp?id=37267"><i>acceleration via monotonicity</i></a>
        <ul><li>Invocation: <code>loat-static --acceleration mon $INPUT</code></li></ul></li>
      <li><a href="https://www.starexec.org/starexec/secure/details/job.jsp?id=37266"><i>acceleration via metering functions</i></a>
        <ul><li>Invocation: <code>loat-static --acceleration meter $INPUT</code></li></ul></li>
      <li><a href="https://www.starexec.org/starexec/secure/details/job.jsp?id=37264">restricted version</a> of our acceleration calculus without <i>acceleration via eventual increase</i>
        <ul><li>Invocation: <code>loat-static --acceleration no-ev-inc $INPUT</code></li></ul></li>
      <li><a href="https://www.starexec.org/starexec/secure/details/job.jsp?id=37263">restricted version</a> of our acceleration calculus without <i>acceleration via eventual decrease</i>
        <ul><li>Invocation: <code>loat-static --acceleration no-ev-dec $INPUT</code></li></ul></li>
      <li><a href="https://www.starexec.org/starexec/secure/details/job.jsp?id=37268">restricted version</a> of our acceleration calculus without <i>acceleration via eventual increase</i> and without <i>acceleration via eventual decrease</i>
        <ul><li>Invocation: <code>loat-static --acceleration no-ev-mon $INPUT</code></li></ul></li>
      <li><a href="https://www.starexec.org/starexec/secure/details/job.jsp?id=37742">Flata</a>
        <ul><li>Invocation: <code>java -cp flata.jar:antlr-3.3-complete.jar:nts.jar verimag.main.Calculator input.rel -noGLPK</code></li></ul></li>
    </ul>

    <p>
      In the tables on StarExec, the result "YES" means that the loop in question was accelerated exactly, "MAYBE" means that it was accelerated approximately, and "NO" means that the tool failed to accelerate it. By clicking on one of the examples and unfolding "output", you can see the full output of the tool.
    </p>

    <h3>LoAT's Output</h3>
    <p>
      If the loop was accelerated successfully, then the end of the output looks, e.g., as follows:
    </p>

    <p>
      <code>
        0.00/0.12	   Start location: start<br/>
        0.00/0.12	      0: start -> f : [], cost: 0<br/>
        0.00/0.12	      2: f -> f : x'=-n+x, x_1'=n+x_1, x_2'=x_3, x_4'=x_5, [ n>0 &amp;&amp; 1+x_1>0 &amp;&amp; x_3>0 &amp;&amp; x_2>0 &amp;&amp; 1-n+x>0 &amp;&amp; -1+x_4>0 &amp;&amp; -1+x_5>0 ], cost: 1<br/>
        0.00/0.12	EOF
      </code>
    </p>

    <p>
      The leading <code>0.00/0.12</code> is a timestamp which is added by StarExec and can thus be ignored, just as the trailing <code>EOF</code>.
      The accelerated loop is presented in a rule-based formalism, which is equivalent to the formulas that are used in the paper.
      It is always prefixed by <code>c: f -> f</code> where <code>c</code> is a natural number.
      The remainder of the corresponding line above is equivalent to the formula
    </p>
    <p>
      <code>x'=-n+x &amp;&amp; x_1'=n+x_1 &amp;&amp; x_2'=x_3 &amp;&amp; x_4'=x_5 &amp;&amp; n>0 &amp;&amp; 1+x_1>0 &amp;&amp; x_3>0 &amp;&amp; x_2>0 &amp;&amp; 1-n+x>0 &amp;&amp; -1+x_4>0 &amp;&amp; -1+x_5>0</code>.
    </p>
    <p>
      The costs are irrelevant for our paper and can thus be ignored.
    </p>

    <h3>Flata's Results</h3>
    <p>
      The invocation of Flata was suggested by its developers.
      Note that Flata sometimes failed with one of the following two errors:
    </p>
    <ul>
      <li><code>Exception in thread "main" verimag.flata.common.NotPresburger</code></li>
      <li><code>no viable alternative at character '2'</code></li>
    </ul>
    <p>This happens when the loop contains non-linear arithmetic, which is not supported by Flata.</p>

    <h3>Zip-Files with Results</h3>
    <p>
      As StarExec might be temporarily unavailable due to updates, we also provide zip-files with the results and the full output of LoAT and Flata.
    </p>
    <ul>
      <li>full version of our acceleration calculus
        <ul>
          <li><a href="jobs/calc_info.zip">results</a></li>
          <li><a href="jobs/calc_output.zip">full output</a></li>
        </ul>
      </li>
      <li><i>acceleration via monotonicity</i>
        <ul>
          <li><a href="jobs/mon_info.zip">results</a></li>
          <li><a href="jobs/mon_output.zip">full output</a></li>
        </ul>
      </li>
      <li><i>acceleration via metering functions</i>
        <ul>
          <li><a href="jobs/meter_info.zip">results</a></li>
          <li><a href="jobs/meter_output.zip">full output</a></li>
        </ul>
      </li>
      <li>restricted version of our acceleration calculus without <i>acceleration via eventual increase</i>
        <ul>
          <li><a href="jobs/no_ev_inc_info.zip">results</a></li>
          <li><a href="jobs/no_ev_inc_output.zip">full output</a></li>
        </ul>
      </li>
      <li>restricted version of our acceleration calculus without <i>acceleration via eventual decrease</i>
        <ul>
          <li><a href="jobs/no_ev_dec_info.zip">results</a></li>
          <li><a href="jobs/no_ev_dec_output.zip">full output</a></li>
        </ul>
      </li>
      <li>restricted version of our acceleration calculus without <i>acceleration via eventual increase</i> and without <i>acceleration via eventual decrease</i>
        <ul>
          <li><a href="jobs/no_ev_mon_info.zip">results</a></li>
          <li><a href="jobs/no_ev_mon_output.zip">full output</a></li>
        </ul>
      </li>
      <li>Flata
        <ul>
          <li><a href="jobs/flata_info.zip">results</a></li>
          <li><a href="jobs/flata_output.zip">full output</a></li>
        </ul>
      </li>
    </ul>

    <h3>Detailed Results</h3>

    Below we provide tables with the detailed results of our benchmarks:
    <ul>
      <li><a href="./accel/loat.html">LoAT</a></li>
      <li><a href="./accel/monot.html"><i>acceleration via monotonicity</i></a></li>
      <li><a href="./accel/meter.html"><i>acceleration via metering functions</i></a></li>
      <li><a href="./accel/flata.html">Flata</a></li>
      <li><a href="./accel/loat_no_ev_inc.html">LoAT without <i>acceleration via eventual increase</i></a></li>
      <li><a href="./accel/loat_no_ev_dec.html">LoAT without <i>acceleration via eventual decrease</i></a></li>
      <li><a href="./accel/loat_no_ev_mon.html">LoAT without <i>acceleration via eventual increase</i> and <i>acceleration via eventual decrease</i></a></li>
    </ul>

    <h3>LoAT's Input Format</h3>

    <p>
      LoAT uses the <a href="http://aprove.informatik.rwth-aachen.de/eval/IntegerComplexity-Journal/">input format of the tool KoAT</a> (file ending .koat).
      It represents programs as transition systems, using a rule-based formalism. An example for a valid input is:
    </p>

    <p>
      <code>
        (GOAL COMPLEXITY)<br/>
        (STARTTERM (FUNCTIONSYMBOLS start))<br/>
        (VAR x y z)<br/>
        (RULES<br/>
        &nbsp;&nbsp;start(x, y, z) -> f(x, y, z)<br/>
        &nbsp;&nbsp;f(x, y, z) -> f(x-1, y+x, z-y) [x > 0 &amp;&amp; y > 0 &amp;&amp; z > 0]<br/>
        )
      </code>
    </p>

    <p>
      The first line is needed for historical reasons and is meaningless in the context of our paper.
    </p>

    <p>
      The second line declares the entry-point of the program. Note that KoAT's input format requires that each program has a unique entry-point without any incoming transitions (i.e., in the example above, a rule where <code>start</code> occurs on the
      right-hand side would be invalid).
    </p>

    <p>
      In the third line, the program variables are declared.
    </p>

    <p>
      For the purpose of our paper, the <code>RULES</code>-section always contains two rules: One of the form
    </p>

    <p>
      <code>
        start(...) -> f(...),
      </code>
    </p>

    <p>
      which is needed due to the requirement that the entry-point of the program does not have incoming transitions (see above), and a second rule
    </p>

    <p>
      <code>
        f(x_1,...,x_d) -> f(t_1,...,t_d) [phi],
      </code>
    </p>

    <p>
      which represents the loop that should be accelerated. More precisely, it represents the following loop:
    </p>

    <p>
      <code>
        while (phi)<br/>
        &nbsp;&nbsp;x_1 := t_1<br/>
        &nbsp;&nbsp;...<br/>
        &nbsp;&nbsp;x_d := t_d
      </code>
    </p>

    <h1 id="nonterm"><a href="https://arxiv.org/abs/2202.04546">A Calculus for Modular Loop Acceleration and Non-Termination Proofs</a></h1>

    <p>
      For our evaluation of our novel calculus for loop acceleration, see <a href="index.html#accel">above</a>.
      In the following, we provide information about the evaluation of our novel calculus for proving non-termination.
    </p>

    <h2>Downloading LoAT</h2>

    <p>
      We provide a
      <a href="https://github.com/aprove-developers/LoAT/releases/tag/sttt21">pre-compiled binary of LoAT (Linux, 64 bit)</a>.
      Apart from that, LoAT is open-source and the source code of the version that was used for our evaluation is available on <a href="https://github.com/aprove-developers/LoAT/tree/sttt21">Github</a>.
    </p>


    <h2>Examples</h2>

    <ul>
      <li><a href="loops_smt.zip">Here</a> you can find the loops that we used for our evaluation.</li>
      <li><a href="loops_c.zip">Here</a> you can find the loops that we used for our evaluation as <code>C</code> programs.</li>
      <li><a href="examples_nonterm.zip">Here</a> you can find the examples from our paper.</li>
    </ul>

    <p>
      The examples that could not be solved by any tool in our evaluation are:
    </p>
    <ul>
      <li><code>1567523084804575.koat</code></li>
      <li><code>1567523106272845.koat</code></li>
      <li><code>1567523084803520.koat</code></li>
      <li><code>1567523039443195.koat</code></li>
    </ul>

    <h2>Evaluation</h2>

    <h3>Versions of Other Tools</h3>

    <ul>
      <li>For AProVE, we used a <a href="aprove.jar">custom version provided by its developers</a>.</li>
      <li>For iRankFinder, we used the <a href="https://www.starexec.org/starexec/secure/details/solver.jsp?id=29509">version from the termination competition 2021</a>.</li>
      <li>For RevTerm, we used the version with SHA <code>45e96f9</code> from the <a href="https://github.com/ekgma/RevTerm">GitHub repository</a>.</li>
      <li>For Ultimate, we used the <a href="https://www.starexec.org/starexec/secure/details/solver.jsp?id=33900">version from the termination competition 2021</a>.</li>
      <li>For VeryMax, we used the <a href="https://www.starexec.org/starexec/secure/details/solver.jsp?id=9339">version from the termination competition 2019</a>.</li>
    </ul>

    <h3>Invoking the Tools</h3>

    <p>
      Below we show how to invoke the different tools and configurations that we evaluated.
    </p>
    <ul>
      <li>LoAT: <code>loat-static --mode recurrent_set $INPUT</code></li>
      <li>AProVE: <code>java -Xmx14G -Xms14G -ea -jar aprove.jar -m wst -w 4 $INPUT</code></li>
      <li>AProVE NT: <code>java -Xmx14G -Xms14G -ea -jar aprove.jar -m wst -w 4 -s llvm-nonterm.strategy $INPUT</code>
        <ul>
          <li>you can find the file <code>llvm-nonterm.strategy</code> <a href="llvm-nonterm.strategy">here</a></li>
        </ul>
      </li>
      <li>iRankFinder: StarExec-configuration <code>competition</code></li>
      <li>iRankFinder NT: <code>irankfinder -nt monotonicrecset -f $INPUT</code></li>
      <li>RevTerm: we used the following two invocations, where the first one was wrapped with <code>timeout 30</code>
        <ul>
          <li><code>RevTerm.sh $INPUT -linear part1 mathsat 2 1</code></li>
          <li><code>RevTerm.sh $INPUT -linear part2 mathsat 2 1</code></li>
        </ul>
      </li>
      <li>Ultimate: StarExec-Configuration <code>default</code></li>
      <li>VeryMax: StarExec-Configuration <code>termcomp19_ITS</code></li>
      <li>LoAT without <i>monotonic increase</i>: <code>loat-static --mode recurrent_set_no_inc $INPUT</code></li>
      <li>LoAT without <i>eventual increase</i>: <code>loat-static --mode recurrent_set_no_ev_inc $INPUT</code></li>
      <li>LoAT without <i>fixpoints</i>: <code>loat-static --mode recurrent_set_no_fp $INPUT</code></li>
      <li>LoAT without <i>eventual increase</i> and <i>fixpoints</i>: <code>loat-static --mode recurrent_set_trivial $INPUT</code></li>
    </ul>

    <h3>Detailed Results</h3>

    Below we provide tables with the detailed results of our benchmarks:
    <ul>
      <li><a href="./nonterm/loat.html">LoAT</a></li>
      <li><a href="./nonterm/aprove.html">AProVE</a></li>
      <li><a href="./nonterm/aprove_nt.html">AProVE NT</a></li>
      <li><a href="./nonterm/irankfinder.html">iRankFinder</a></li>
      <li><a href="./nonterm/irankfinder_nt.html">iRankFinder NT</a></li>
      <li><a href="./nonterm/revterm.html">RevTerm</a></li>
      <li><a href="./nonterm/ultimate.html">Ultimate</a></li>
      <li><a href="./nonterm/verymax.html">VeryMax</a></li>
      <li><a href="./nonterm/loat_no_inc.html">LoAT without <i>monotonic increase</i></a></li>
      <li><a href="./nonterm/loat_no_ev_inc.html">LoAT without <i>eventual increase</i></a></li>
      <li><a href="./nonterm/loat_no_fp.html">LoAT without <i>fixpoints</i></a></li>
      <li><a href="./nonterm/loat_trivial.html">LoAT without <i>eventual increase</i> and <i>fixpoints</i></a></li>
    </ul>

  </body>
</html>
